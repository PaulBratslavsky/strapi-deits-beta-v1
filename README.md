## You can give it a try by installing Strapi 4.6.0-beta.1


``` bash
    npx create-strapi-app@4.6.0-beta.1
```

Once you create your content type and dummy data you can export it by using the CLI commands.

Our content type structure.

![[Screenshot 2023-01-10 at 6.00.27 PM.png]]

Here we have added our dummy data.

![[Screenshot 2023-01-10 at 5.59.30 PM.png]]

Notice our post has a relationship to admin user.

![[Screenshot 2023-01-10 at 6.01.38 PM.png]]

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

![[Screenshot 2023-01-10 at 5.42.20 PM.png]]
You can unpack the file and take a look inside.![[Screenshot 2023-01-10 at 5.44.35 PM.png]]
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

![[Screenshot 2023-01-10 at 5.53.34 PM.png]]

We can see here that our user realationship is mising.

![[Screenshot 2023-01-10 at 5.54.40 PM.png]]

Currently the import does not generate your schema so your target Strapi project should have matching schema and content types.