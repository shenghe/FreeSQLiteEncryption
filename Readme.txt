The Free SQLite Encryption Extension (FSEE)
======================

Sources
==================================

* SQLite 3.7.14.1 : <http://www.sqlite.org/sqlite-amalgamation-3071401.zip>
* Wxsqlite3-3.0.0.1 ：<http://sourceforge.net/projects/wxcode/files/Components/wxSQLite3/>

Build
==================================
Use vs2012 or vs2010 to compile the solution

Update By Yourself
==================================

1. Download the lasted SQLite. Unzip it to the "sqlite3" folder.
2. Download the lasted wxsqlite3. Unzip the “wxsqlite3-3.x.x.x\wxsqlite3-3.x.x\sqlite3\secure\src” folder to "sqlite3".
3. Use vs2012 or vs2010(not tested) to compile the solution.
4. In the bin folder,you will find the "sqlite.dll" and "sqlite.lib"
5. You can use the "sqlite3_key" and "sqlite3_rekey" API

API
==================================

int sqlite3_key( sqlite3 *db, const void *pKey, int nKey)
int sqlite3_rekey( sqlite3 *db, const void *pKey, int nKey)

Thanks
==================================

* sqlite(http://www.sqlite.org/)
* Wxcode(http://wxcode.sourceforge.net/)
* chengyoufan(http://download.csdn.net/detail/chengyoufan/3463637)
