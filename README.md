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

### 8. Menginputkan 3 data ke dalam collection `student` beserta reference ke `departemen`.

input:
```
db.student.insert([
  {
    nim: "21212018",
    name: "Didit Suryadi",
    address: "Jalan Surya Kencana, Bogor",
    department: {
      $ref : "department",
      $id : ObjectId("58901756ca49c7522b60680f"),
      $db : "academic"
    }
  },
  {
    nim: "2001600595",
    name: "Didit Suryadi",
    address: "Jalan kemanggisan ilir 3",
    department: {
      $ref : "department",
      $id : ObjectId("58b6364260f3a0eac681ad21"),
      $db : "academic"
    }
  },
  {
    nim: "256789332",
    name: "Aditya Kesuma",
    address: "Bogor",
    department: {
      $ref : "department",
      $id : ObjectId("58b6364260f3a0eac681ad1f"),
      $db : "academic"
    }
  },
  ]);
```
output:

```
BulkWriteResult({
       	"writeErrors" : [ ],
       	"writeConcernErrors" : [ ],
       	"nInserted" : 3,
       	"nUpserted" : 0,
       	"nMatched" : 0,
       	"nModified" : 0,
       	"nRemoved" : 0,
       	"upserted" : [ ]
})
```
### 9. Melihat isi collection `student`.

input:
`db.student.find().pretty()`

output:
```
{
	"_id" : ObjectId("58b6353b60f3a0eac681ad1c"),
	"nim" : "21210018006",
	"name" : "Didit Suryadi",
	"address" : "kemanggisan ilir 3",
	"department" : "FT"
}
{
	"_id" : ObjectId("58b637601259b55674c8a839"),
	"nim" : "21212018",
	"name" : "Didit Suryadi",
	"address" : "Jalan Surya Kencana, Bogor",
	"department" : DBRef("department", ObjectId("58901756ca49c7522b60680f"), "academic")
}
{
	"_id" : ObjectId("58b637601259b55674c8a83a"),
	"nim" : "2001600595",
	"name" : "Didit Suryadi",
	"address" : "Jalan kemanggisan ilir 3",
	"department" : DBRef("department", ObjectId("58b6364260f3a0eac681ad21"), "academic")
}
{
	"_id" : ObjectId("58b637601259b55674c8a83b"),
	"nim" : "256789332",
	"name" : "Aditya Kesuma",
	"address" : "Bogor",
	"department" : DBRef("department", ObjectId("58b6364260f3a0eac681ad1f"), "academic")
}
```

### 10. Menampilkan key `name` dan `address` dalam collection ```student```.

input:
```
db.student.find({},{"name": 1,"address": 1}).pretty();
```

output:
```
{
	"_id" : ObjectId("58b6353b60f3a0eac681ad1c"),
	"name" : "Didit Suryadi",
	"address" : "kemanggisan ilir 3"
}
{
	"_id" : ObjectId("58b637601259b55674c8a839"),
	"name" : "Didit Suryadi",
	"address" : "Jalan Surya Kencana, Bogor"
}
{
	"_id" : ObjectId("58b637601259b55674c8a83a"),
	"name" : "Didit Suryadi",
	"address" : "Jalan kemanggisan ilir 3"
}
{
	"_id" : ObjectId("58b637601259b55674c8a83b"),
	"name" : "Aditya Kesuma",
	"address" : "Bogor"
}
```
### 11. Menampilkan key ```StudentId```, ```name```, dan ```address``` dari data student yang mempunyai ```studentId``` tertentu.

input:
```
db.student.find({nim:"256789332"},{"nim": 1,"name": 1,"address":1}).pretty();
```

output:
```
{
	"_id" : ObjectId("58b637601259b55674c8a83b"),
	"nim" : "256789332",
	"name" : "Aditya Kesuma",
	"address" : "Bogor"
}
```
### 12. Menampilkan semua data ```student``` secara urut berdasarkan ```name``` dengan ```sort()``` secara ascending maupun descending.

input:
```
db.student.find().sort({name:1}).pretty();
db.student.find().sort({name:-1}).pretty();
```

output:
```
{
	"_id" : ObjectId("58b637601259b55674c8a83b"),
	"nim" : "256789332",
	"name" : "Aditya Kesuma",
	"address" : "Bogor",
	"department" : DBRef("department", ObjectId("58b6364260f3a0eac681ad1f"), "academic")
}
{
	"_id" : ObjectId("58b6353b60f3a0eac681ad1c"),
	"nim" : "21210018006",
	"name" : "Didit Suryadi",
	"address" : "kemanggisan ilir 3",
	"department" : "FT"
}
{
	"_id" : ObjectId("58b637601259b55674c8a839"),
	"nim" : "21212018",
	"name" : "Didit Suryadi",
	"address" : "Jalan Surya Kencana, Bogor",
	"department" : DBRef("department", ObjectId("58901756ca49c7522b60680f"), "academic")
}
{
	"_id" : ObjectId("58b637601259b55674c8a83a"),
	"nim" : "2001600595",
	"name" : "Didit Suryadi",
	"address" : "Jalan kemanggisan ilir 3",
	"department" : DBRef("department", ObjectId("58b6364260f3a0eac681ad21"), "academic")
}
```
```
{
	"_id" : ObjectId("58b6353b60f3a0eac681ad1c"),
	"nim" : "21210018006",
	"name" : "Didit Suryadi",
	"address" : "kemanggisan ilir 3",
	"department" : "FT"
}
{
	"_id" : ObjectId("58b637601259b55674c8a839"),
	"nim" : "21212018",
	"name" : "Didit Suryadi",
	"address" : "Jalan Surya Kencana, Bogor",
	"department" : DBRef("department", ObjectId("58901756ca49c7522b60680f"), "academic")
}
{
	"_id" : ObjectId("58b637601259b55674c8a83a"),
	"nim" : "2001600595",
	"name" : "Didit Suryadi",
	"address" : "Jalan kemanggisan ilir 3",
	"department" : DBRef("department", ObjectId("58b6364260f3a0eac681ad21"), "academic")
}
{
	"_id" : ObjectId("58b637601259b55674c8a83b"),
	"nim" : "256789332",
	"name" : "Aditya Kesuma",
	"address" : "Bogor",
	"department" : DBRef("department", ObjectId("58b6364260f3a0eac681ad1f"), "academic")
}
```
### 13. Menampilkan semua data ```department``` secara urut berdasarkan ```name``` secara ascending maupun descending.

input:
```
db.department.find().sort({name:1}).pretty();
db.department.find().sort({name:-1}).pretty();
```

output:
```
{
	"_id" : ObjectId("58b6364260f3a0eac681ad1e"),
	"code" : "FEK",
	"name" : "Fakultas Ekonomi dan Komunikasi",
	"major" : [
		{
			"name" : "Akuntansi"
		},
		{
			"name" : "Keuangan"
		},
		{
			"name" : "Komunikasi Pemasaran"
		}
	]
}
{
	"_id" : ObjectId("58b6364260f3a0eac681ad21"),
	"code" : "FT",
	"name" : "Fakultas Teknik",
	"major" : [
		{
			"name" : "Arsitektur"
		},
		{
			"name" : "Teknik Industri"
		},
		{
			"name" : "Teknik Komputer"
		}
	]
}
{
	"_id" : ObjectId("58b6364260f3a0eac681ad1d"),
	"code" : "FTI",
	"name" : "Fakultas Teknik Informatika",
	"major" : [
		{
			"name" : "Sistem Informasi"
		},
		{
			"name" : "Teknik Informatika"
		}
	]
}
{
	"_id" : ObjectId("58b6364260f3a0eac681ad20"),
	"code" : "SBM",
	"name" : "Sekolah Bisnis dan Manajemen",
	"major" : [
		{
			"name" : "Bisnis & Manajemen Internasional"
		},
		{
			"name" : "Manajeman"
		},
		{
			"name" : "Pemasaran Internasional"
		}
	]
}
{
	"_id" : ObjectId("58b6364260f3a0eac681ad1f"),
	"code" : "SD",
	"name" : "Sekolah Design",
	"major" : [
		{
			"name" : "Desain Interior"
		},
		{
			"name" : "Desain Komunikasi Visual"
		},
		{
			"name" : "Desain Komunikasi Visual Media Baru"
		}
	]
}
```
```
{
	"_id" : ObjectId("58b6364260f3a0eac681ad1f"),
	"code" : "SD",
	"name" : "Sekolah Design",
	"major" : [
		{
			"name" : "Desain Interior"
		},
		{
			"name" : "Desain Komunikasi Visual"
		},
		{
			"name" : "Desain Komunikasi Visual Media Baru"
		}
	]
}
{
	"_id" : ObjectId("58b6364260f3a0eac681ad20"),
	"code" : "SBM",
	"name" : "Sekolah Bisnis dan Manajemen",
	"major" : [
		{
			"name" : "Bisnis & Manajemen Internasional"
		},
		{
			"name" : "Manajeman"
		},
		{
			"name" : "Pemasaran Internasional"
		}
	]
}
{
	"_id" : ObjectId("58b6364260f3a0eac681ad1d"),
	"code" : "FTI",
	"name" : "Fakultas Teknik Informatika",
	"major" : [
		{
			"name" : "Sistem Informasi"
		},
		{
			"name" : "Teknik Informatika"
		}
	]
}
{
	"_id" : ObjectId("58b6364260f3a0eac681ad21"),
	"code" : "FT",
	"name" : "Fakultas Teknik",
	"major" : [
		{
			"name" : "Arsitektur"
		},
		{
			"name" : "Teknik Industri"
		},
		{
			"name" : "Teknik Komputer"
		}
	]
}
{
	"_id" : ObjectId("58b6364260f3a0eac681ad1e"),
	"code" : "FEK",
	"name" : "Fakultas Ekonomi dan Komunikasi",
	"major" : [
		{
			"name" : "Akuntansi"
		},
		{
			"name" : "Keuangan"
		},
		{
			"name" : "Komunikasi Pemasaran"
		}
	]
}
```
