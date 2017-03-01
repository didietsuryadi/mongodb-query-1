# mongodb-query

### 1. Membuat database `academic`

input:

`use academic`

output:

```
> use academic
switched to db academic
```

### 2. Menampilkan semua collection dan data dalam database

input:

`show collections`

output:

```
> show collections
>
```

### 3. Membuat atau mengaktifkan database

input:

`use academic`

output:

```
> use academic
switched to db academic
```

### 4. Membuat collection `departemen`.

input:

`> db.createCollection("department")`

output:

```
{ "ok" : 1 }
```

### 5. Membuat collection `student`.

input:

`> db.createCollection("student")`

output:

```
{ "ok" : 1 }
```

### 6. Melihat struktur collection `student`.

input:
```
> db.student.insert({nim:"21210018006", name:"Didit Suryadi", address:"kemanggisan ilir 3", department:"FT"})
> var schema = db.student.findOne()
> for(var key in schema){print (key, typeof key);}
```

output:
```
_id string
nim string
name string
address string
department string
```

### 7. Menginputkan 5 data ke dalam collection `departemen`.

```
db.department.insert([
  {
    code: "FTI",
    name: "Fakultas Teknik Informatika",
    major: [{name: "Sistem Informasi"},{name: "Teknik Informatika"}]
  },
  {
    code: "FEK",
    name: "Fakultas Ekonomi dan Komunikasi",
    major:[{name: "Akuntansi"}, {name: "Keuangan"}, {name: "Komunikasi Pemasaran"}]
  },
  {
    code: "SD",
    name: "Sekolah Design",
    major: [{name: "Desain Interior"},{name: "Desain Komunikasi Visual"},{name: "Desain Komunikasi Visual Media Baru"}]
  },
  {
    code: "SBM",
    name: "Sekolah Bisnis dan Manajemen",
    major:[{name: "Bisnis & Manajemen Internasional"}, {name: "Manajeman"}, {name: "Pemasaran Internasional"}]
  },
  {
    code: "FT",
    name: "Fakultas Teknik",
    major: [{name: "Arsitektur"},{name: "Teknik Industri"},{name: "Teknik Komputer"}]
  }]
  );
```
output:

```
BulkWriteResult({
       	"writeErrors" : [ ],
       	"writeConcernErrors" : [ ],
       	"nInserted" : 5,
       	"nUpserted" : 0,
       	"nMatched" : 0,
       	"nModified" : 0,
       	"nRemoved" : 0,
       	"upserted" : [ ]
})
```
