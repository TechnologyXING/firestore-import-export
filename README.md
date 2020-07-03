# Firestore Import Export
A script that help to export and import in Cloud Firestore

THIS IS A fork of [@dalenguyen/firestore-import-export](https://github.com/dalenguyen/firestore-import-export)

# Changes from forked version as of July 3, 2020 at 7:25PM PhST
 - use of .env instead of hard-coded url, so there's only one place to edit.
 - fixed subCollection name when using sub collections
 - exported (downloaded) data is "prettified" using tabs, remove ```PRETTIFIED=1``` from the ```.env``` if you just want the regular JSON string.

# Requirements

You need [NODE](https://nodejs.org/en/download/) or something that can run JAVASCRIPT (JS) file.

Get **serviceAccount** JSON file from *Project Setting > SERVICE ACCOUNTS* in Firebase Console

# Setting Up

Download or clone this repository

```
git clone https://github.com/TechnologyXING/firestore-import-export.git
```

Install NPM packages

```
npm install
```

# Create a ```.env``` file in the root directory (besides ```package.json```)
The file should contain the following where _https://*******.firebaseio.com_ is the URL of your Firebase Firestore database.
```
DB_URL=https://*******.firebaseio.com
```
You can get your database url from your **Firebase Console** > Project **Settings** > **General** tab > select your **Web App** below > then in **Firebase SDK snippet** choose **Config** radio button. copy the **databaseURL** without the quotes.

NOTE: in the absence of this configuration, [Firebase Admin](https://firebase.google.com/docs/admin/setup#initialize-without-parameters) will automatically use the database URL saved locally when you installed and configured the **firebase-cli**.

# Export database from Firestore

This will help you create a backup of your collection and subcollection from Firestore to a JSON file name **firestore-export.json**

```
node export.js <your-collection-name> <sub-collection-name-(optional)>
```

# Import database to Firestore

This will import a collection to Firestore will overwrite any documents in that collection with matching id's to those in your json. If you have date type in your JSON, please add the field to the command line. **The date and geo arguments is optional**.

```
node import.js import-to-firestore.json date=date geo=Location
```

If you have date type in your JSON, please add to your command line

Sample from __import-to-firestore.json__. "test" will be the collection name. The date type will have _seconds and _nanoseconds in it.

```
{
  "test" : {
    "first-key" : {
      "email"   : "dungnq@itbox4vn.com",
      "website" : "dalenguyen.me",
      "custom"  : {
        "firstName" : "Dale",
        "lastName"  : "Nguyen"
      },
      "date": {
        "_seconds":1534046400,
        "_nanoseconds":0
      },
      "Location": {
        "_latitude": 49.290683,
        "_longitude": -123.133956
      }
    },
    "second-key" : {
      "email"   : "test@dalenguyen.me",
      "website" : "google.com",
      "custom"  : {
        "firstName" : "Harry",
        "lastName"  : "Potter"
      },
      "date": {
        "_seconds":1534262435,
        "_nanoseconds":0
      },
      "Location": {
        "_latitude": 49.290683,
        "_longitude": -123.133956
      }
    }
  }
}
```

Thanks to [@fed239](https://github.com/fed239), you can use YAML files instead of JSON files in order to import to firestore.

*If you have any recommendation or question, please create an issue. Thanks,*
