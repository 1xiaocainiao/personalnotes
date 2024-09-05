使用 **StoreKit 2**，Apple 提供了更多直接在客户端管理订阅和验证收据的功能。StoreKit 2 支持更强大的 API，允许你在没有后端的情况下直接在应用中处理订阅、验证收据，并管理用户的订阅状态。

以下是如何使用 **StoreKit 2** 实现订阅，并验证订阅有效性的详细步骤。

___

### 1\. **设置 StoreKit 2**

首先，确保你已经导入了 StoreKit 2 框架，并确保 Xcode 版本支持 StoreKit 2（iOS 15+）。
```
import StoreKit
```

### 2\. **订阅产品的设置**

#### 2.1 获取订阅产品

在 StoreKit 2 中，你可以使用 `Product` 来加载和处理应用内购买商品。你需要先获取订阅产品的信息。

```
// 获取订阅产品
func fetchProducts() async throws -> [Product] {
    let productIDs = ["your_subscription_product_id"]
    let products = try await Product.products(for: productIDs)
    return products
}

```

#### 2.2 购买订阅

StoreKit 2 提供了更简洁的 API 来进行购买。

```
func purchaseProduct(_ product: Product) async throws -> Transaction? {
    let result = try await product.purchase()
    
    switch result {
    case .success(let verification):
        // 验证交易
        let transaction = try checkVerified(verification)
        // 购买成功，处理订阅
        await transaction.finish()
        return transaction
        
    case .userCancelled:
        // 用户取消购买
        return nil
        
    case .pending:
        // 交易挂起
        return nil
    }
}

// 验证交易
func checkVerified<T>(_ result: VerificationResult<T>) throws -> T {
    switch result {
    case .unverified:
        throw StoreError.failedVerification
    case .verified(let safe):
        return safe
    }
}

```

`purchase()` 方法会返回一个 `Product.PurchaseResult`，你可以根据返回的结果处理成功、取消或挂起的情况。

### 3\. **验证订阅有效性**

StoreKit 2 提供了新的 API 来验证用户的订阅状态，而不需要后端支持。通过 `Transaction.currentEntitlement(for:)` 或 `Product.SubscriptionInfo.Status`，你可以直接在应用中检查用户的订阅是否有效。

#### 3.1 获取订阅状态

使用 `Transaction.currentEntitlement(for:)` 方法来获取用户当前的订阅状态。

```
func checkSubscriptionStatus() async throws -> Bool {
    for await verificationResult in Transaction.currentEntitlements {
        let transaction = try checkVerified(verificationResult)
        
        // 检查产品 ID 是否是订阅产品
        if transaction.productID == "your_subscription_product_id" {
            // 订阅有效
            return true
        }
    }
    
    // 没有有效的订阅
    return false
}

```

`Transaction.currentEntitlements` 是一个异步序列，返回所有当前有效的订阅和购买。你可以通过遍历这些交易来确定用户是否有有效的订阅。

#### 3.2 使用 `SubscriptionInfo` 验证订阅

你也可以使用 `Product.SubscriptionInfo` 来获取订阅的详细信息，例如过期日期和续订状态。

```
func checkSubscriptionDetails(for product: Product) async throws -> Product.SubscriptionInfo.Status? {
    guard let subscription = product.subscription else {
        return nil
    }
    
    let statuses = try await subscription.status
    return statuses.first // 获取第一个订阅状态
}

func isSubscriptionActive(for product: Product) async -> Bool {
    do {
        if let status = try await checkSubscriptionDetails(for: product) {
            switch status.state {
            case .subscribed, .inGracePeriod, .inBillingRetryPeriod:
                return true // 订阅是有效的
            default:
                return false
            }
        }
    } catch {
        print("Error checking subscription status: \(error)")
    }
    return false
}

```

`Product.SubscriptionInfo.Status` 提供了订阅的详细状态，包含订阅是否在续订、宽限期、重试期等。

### 4\. **处理恢复购买**

用户可以通过恢复购买来重新获取他们的订阅权限，尤其是在重新安装应用或者更换设备时。

```
func restorePurchases() async {
    do {
        for await verificationResult in Transaction.currentEntitlements {
            let transaction = try checkVerified(verificationResult)
            // 恢复购买的处理逻辑
            print("Restored transaction: \(transaction)")
        }
    } catch {
        print("Failed to restore purchases: \(error)")
    }
}

```

### 5\. **定期检查订阅状态**

为了在没有后端服务器的情况下保持订阅状态最新，你可以在应用的某些时刻（如启动或进入前台时）定期检查订阅状态：

-   **在应用启动时**：检查订阅状态。
-   **在应用进入前台时**：如果有需要，检查用户的订阅状态。

可以通过应用的生命周期钩子（如 `applicationDidBecomeActive`）进行调用。

```
func applicationDidBecomeActive(_ application: UIApplication) {
    Task {
        let isActive = await checkSubscriptionStatus()
        // 根据订阅状态更新应用 UI
    }
}

```

### 6\. **定期验证收据**

尽管 StoreKit 2 提供了丰富的订阅状态管理，你仍然可以定期获取并验证收据。Apple 建议使用 `Transaction.all` 来遍历并验证所有交易。

```
func validateReceipts() async throws {
    for await result in Transaction.all {
        let transaction = try checkVerified(result)
        print("Transaction ID: \(transaction.id), Product ID: \(transaction.productID)")
        // 可以将收据发送到 Apple 的服务器进行进一步验证
    }
}

```

### 7\. **错误处理**

你需要确保正确处理用户取消购买、交易失败、网络错误等各种情况，提供良好的用户体验。

___

### 总结

-   **订阅管理**：通过 StoreKit 2 的 API，可以在应用内直接获取产品信息、购买订阅和验证订阅状态，甚至无需后端服务器。
    
-   **验证订阅状态**：使用 `Transaction.currentEntitlement(for:)` 和 `Product.SubscriptionInfo.Status` 可以轻松判断订阅是否有效，并根据订阅状态更新用户体验。
    
-   **恢复购买**：使用 `Transaction.currentEntitlements` 来恢复购买记录，确保用户可以在不同设备上获取他们的订阅权限。
    
-   **安全性**：虽然可以在客户端直接验证交易和订阅，但出于安全考虑，仍然要尽量避免在客户端存储敏感数据。定期检查订阅状态，防止用户绕过购买验证。
    

通过 StoreKit 2，你能够在没有后端的情况下实现较为完整的订阅管理和验证。
