The Free SQLite Encryption Extension (FSEE)

The Sources just tested on Windows.

Sources:
1.SQLite 3.7.14.1 : http://www.sqlite.org/sqlite-amalgamation-3071401.zip
2.Wxsqlite3-3.0.0.1 ：http://sourceforge.net/projects/wxcode/files/Components/wxSQLite3/

Usage：
1.Download the lasted SQLite. Unzip it to the "sqlite3" folder.
2.Download the lasted wxsqlite3. Unzip the “wxsqlite3-3.x.x.x\wxsqlite3-3.x.x\sqlite3\secure\src” folder to "sqlite3".
3.Use vs2012 or vs2010(not tested) to compile the solution.
4.In the Release or Debug folder,you will find the "sqlite.dll" and "sqlite.lib"
5.You can use the "sqlite3_key" and "sqlite3_rekey" API

API:
int sqlite3_key( sqlite3 *db, const void *pKey, int nKey)
int sqlite3_rekey( sqlite3 *db, const void *pKey, int nKey)

Thanks:
1.sqlite(http://www.sqlite.org/)
2.Wxcode(http://wxcode.sourceforge.net/)
3.chengyoufan(http://download.csdn.net/detail/chengyoufan/3463637)