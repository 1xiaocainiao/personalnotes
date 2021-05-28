最近数据有修改，添加了字段，需要升级数据库，到这个[原文链接](https://blog.csdn.net/heming9174/article/details/93195718)

特此记录一下
```
static DbManager get instance => _getInstance();
  static DbManager _instance;
  static Database database;
  static String dbName = 'UserInfoCache.db';
  static String userTableName = 'users';

  DbManager._internal() {
    // 初始化
  }

  static DbManager _getInstance() {
    if (_instance == null) {
      _instance = new DbManager._internal();
    }
    return _instance;
  }

  Future<void> openDb() async {
    database = await openDatabase(
      join(await getDatabasesPath(), dbName),
      onCreate: _onCreate,
      onUpgrade: _onUpgrade,
      onDowngrade: onDatabaseDowngradeDelete,
      version: 2,
    );
  }

  void _onCreate(Database db, int version) async {
    var batch = db.batch();
    _createTableCompanyV1(batch);
    _updateTableCompanyV1toV2(batch);

    await batch.commit();
    print("Table is created");
  }

  void _onUpgrade(Database db, int oldVersion, int newVersion) async {
    var batch = db.batch();
    if (oldVersion == 1) {
      _updateTableCompanyV1toV2(batch);
    }
    await batch.commit();
  }

  void _createTableCompanyV1(Batch batch) {
    batch.execute(
      "CREATE TABLE $userTableName(user_id TEXT PRIMARY KEY, realname TEXT, avatar TEXT, type TEXT, is_vip TEXT ) ",
    );
  }

  ///更新数据库Version: 1->2.
  void _updateTableCompanyV1toV2(Batch batch) {
    batch.execute('ALTER TABLE $userTableName ADD is_super_like_me TEXT');
  }

  Future<void> setUserInfo(IMUserInfo info) async {
    if (database == null) {
      await openDb();
    }
    await database?.insert(userTableName, info.toJson(),
        conflictAlgorithm: ConflictAlgorithm.replace);
  }

  Future<List<IMUserInfo>> getUserInfo({String userId}) async {
    List<Map<String, dynamic>> maps = List();
    if (database == null) {
      await openDb();
    }
    if (userId == null || userId.isEmpty) {
      maps = await database?.query(userTableName);
    } else {
      maps = await database
          ?.query(userTableName, where: 'user_id = ?', whereArgs: [userId]);
    }
    List<IMUserInfo> infoList = List();
    if (maps.length > 0) {
      infoList = List.generate(maps.length, (i) {
        IMUserInfo info = IMUserInfo.fromJson(maps[i]);
        return info;
      });
    }
    return infoList;
  }
```
