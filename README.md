# MongoDB_Course
MongoDB Course Training 1 Day

ทดสอบสร้าง Collection  ใหม่เข้าไปใน database เปล่าตามคำสั่งด้านล่างค่ะ

db.createCollection("Students", {
   validator: {
      $jsonSchema: {
         bsonType: "object",
         title: "Student Object Validation",
         required: [ "address", "major", "name", "year" ],
         properties: {
            name: {
               bsonType: "string",
               description: "'name' must be a string and is required"
            },
            year: {
               bsonType: "int",
               minimum: 2017,
               maximum: 3017,
               description: "'year' must be an integer in [ 2017, 3017 ] and is required"
            },
            gpa: {
               bsonType: [ "double" ],
               description: "'gpa' must be a double if the field exists"
            }
         }
      }
   }
} )

ข้างล่างเป็นคำสั่ง Insert 3 Documents เข้าไปยัง Collection :

--------------------- เริ่มต้น CRUD ------------------------
db.Students.insertOne( {
   name: "Alice",
   year: Int32( 2019 ),
   major: "History",
   gpa: Int32(3),
   address: {
      city: "NYC",
      street: "33rd Street"
   },
   Flags: null
} )


db.Students.insertOne( {
   name: "Alice",
   year: Int32( 2019 ),
   major: "History",
   gpa: Int32(3),
   address: {
      city: "NYC",
      street: "33rd Street"
   }
} )


db.Students.insertOne( {
   name: "Alice",
   year: NumberInt(2019),
   major: "History",
   gpa: Double(3.0),
   address: {
      city: "NYC",
      street: "33rd Street"
   }
} )

ตัวอย่างคำสั่งอื่นๆ ดังข้างล่าง
-----------------------rename collection--------------------------

db.Accounts.renameCollection("accounts");

-----------------------rename field--------------------------

db.students.updateMany( {}, { $rename: { "nmae": "name" } } )

db.students.updateOne( { _id: 1 }, { $rename: { "name.first": "name.fname" } } )

db.students.updateMany( {}, { $rename: { "name.first": "name.fname" } } )

--------------------- CRUD แบบ Read หรือ Text Search  ------------------------

db.students.find( { year: { $exists: true, $in: [ 2010, 2019 ] } } )

db.students.find( { name: null } )



