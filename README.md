## You can give it a try by installing Strapi 4.6.0-beta.1


``` bash
    npx create-strapi-app@4.6.0-beta.1
```

Once you create your content type and dummy data you can export it by using the CLI commands.

Our content type structure.

![Screenshot 2023-01-10 at 6 00 27 PM](https://user-images.githubusercontent.com/6153188/211882984-904f2cae-0317-40c5-92b3-4bd85e949fe5.png)

Here we have added our dummy data.

![Screenshot 2023-01-10 at 5 59 30 PM](https://user-images.githubusercontent.com/6153188/211883058-7ac4ebab-bf53-4ff6-9ae7-d9c91771b8b4.png)

Notice our post has a relationship to admin user.

![Screenshot 2023-01-10 at 6 01 38 PM](https://user-images.githubusercontent.com/6153188/211883148-caab7ae6-f885-498d-8973-c73644ae4406.png)

You can run th following command to see all available options:
``` bash
	yarn strapi help export
```

Output: 
``` bash
Usage: strapi export [options]

Export data from Strapi to file

Options:
  --no-encrypt        Disables 'aes-128-ecb' encryption of the output file
  --no-compress       Disables gzip compression of output file
  -k, --key <string>  Provide encryption key in command instead of using the
                      prompt
  -f, --file <file>   name to use for exported file (without extensions)
  -h, --help          Display help for command
✨  Done in 0.45s.
```

We will do the most basic export without password or encryption:
``` bash
	yarn strapi export --no-encrypt -f ../export-no-encrypt
```

We should see this output:
``` bash
	Starting export...
┌─────────────────────────────────────────┬───────┬───────────────┐
│ Type                                    │ Count │ Size          │
├─────────────────────────────────────────┼───────┼───────────────┤
│ schemas                                 │    12 │      15.6 KB  │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- contentType                          │    12 │ (    15.6 KB) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ entities                                │    20 │      11.2 KB  │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- api::post.post                       │     4 │ (     2.9 KB) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- plugin::i18n.locale                  │     1 │ (     158 B ) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- plugin::upload.file                  │     4 │ (       6 KB) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- plugin::users-permissions.permission │     9 │ (     1.7 KB) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- plugin::users-permissions.role       │     2 │ (     466 B ) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ assets                                  │    20 │         9 MB  │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- .jpg                                 │    20 │ (       9 MB) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ links                                   │    13 │       2.6 KB  │
├─────────────────────────────────────────┼───────┼───────────────┤
│ configuration                           │    21 │      55.3 KB  │
├─────────────────────────────────────────┼───────┼───────────────┤
│ Total                                   │    86 │         9 MB  │
└─────────────────────────────────────────┴───────┴───────────────┘
Export process has been completed successfully!
Export archive is in ../export-no-encrypt.tar.gz
✨  Done in 1.60s.
```

We will not have a ***export-no-encrypt.tar.gz*** file with the data.

<img width="974" alt="Screenshot 2023-01-10 at 5 42 20 PM" src="https://user-images.githubusercontent.com/6153188/211883280-88b966dc-e6f4-4c34-b87f-2f705d57fdaf.png">

You can unpack the file and take a look inside.<img width="905" alt="Screenshot 2023-01-10 at 5 44 35 PM" src="https://user-images.githubusercontent.com/6153188/211883336-caf30e6c-b032-44e8-9514-7772455bf20d.png">

Our mane data will be stored in `JSONL` file format.

Let's now delete our local database and files.

You can run the following command to see all import flags available to you:
``` bash
	yarn strapi help import
```

You will see these available options:
``` bash

Usage: strapi import [options]

Import data from file to Strapi

Options:
  -f, --file <file>   path and filename for the Strapi export file you want to
                      import
  -k, --key <string>  Provide encryption key in command instead of using the
                      prompt
  -h, --help          Display help for command
✨  Done in 0.35s.
```

Let's now import our data from our `tar.gz` file by running the following command:
``` bash
	yarn strapi import -f ../export-no-encrypt.tar.gz
```

We will see the following output:
``` bash
	? The import will delete all data in your database. Are you sure you want to
proceed? Yes
Starting import...
┌─────────────────────────────────────────┬───────┬───────────────┐
│ Type                                    │ Count │ Size          │
├─────────────────────────────────────────┼───────┼───────────────┤
│ entities                                │    20 │      11.2 KB  │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- api::post.post                       │     4 │ (     2.9 KB) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- plugin::i18n.locale                  │     1 │ (     158 B ) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- plugin::upload.file                  │     4 │ (       6 KB) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- plugin::users-permissions.permission │     9 │ (     1.7 KB) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- plugin::users-permissions.role       │     2 │ (     466 B ) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ assets                                  │    20 │         9 MB  │
├─────────────────────────────────────────┼───────┼───────────────┤
│ -- .jpg                                 │    20 │ (       9 MB) │
├─────────────────────────────────────────┼───────┼───────────────┤
│ links                                   │    13 │       2.6 KB  │
├─────────────────────────────────────────┼───────┼───────────────┤
│ configuration                           │    21 │      55.3 KB  │
├─────────────────────────────────────────┼───────┼───────────────┤
│ Total                                   │    74 │         9 MB  │
└─────────────────────────────────────────┴───────┴───────────────┘
Import process has been completed successfully!
✨  Done in 5.50s.
```

Let's log back into our admin UI and see our data. When loging in you will have to create a new admin user since at the moment that data is not exported.

![Screenshot 2023-01-10 at 5 53 34 PM](https://user-images.githubusercontent.com/6153188/211883500-d6030e05-ac3b-4e2b-a8d0-3a3d5460c9b9.png)

We can see here that our user realationship is mising.

![Screenshot 2023-01-10 at 5 54 40 PM](https://user-images.githubusercontent.com/6153188/211883554-6597bf35-ffac-4a87-84d8-e15239a23712.png)


Currently the import does not generate your schema so your target Strapi project should have matching schema and content types.# strapi-deits-beta-v1
