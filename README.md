# supabase-client
A Supabase client for Python. This mirrors the design of [supabase-js](https://github.com/supabase/supabase-js/blob/master/README.md)

[Full documentation: https://keosariel.github.io/2021/08/08/supabase-client-python/](https://keosariel.github.io/2021/08/08/supabase-client-python/)

## Overview
[Supabase](https://supabase.io/) is an Open Source Firebase Alternative that provides the tools and infrastructure you need to develop apps. It lets you
create a backend in less than 2 minutes. The **Supabase-Client** abstracts access the endpoints to the READ, INSERT, UPDATE, and DELETE operations on an existing **table** in your supabase application.

However, this project is base on the [Supabase API](https://supabase.io/docs/guides/api)

## Installation
To install Supabase-Client, simply execute the following command in a terminal:
```
pip install supabase-client
```

## Managing Data

```python

# requirement: pip install python-dotenv

import asyncio
from supabase_client import Client

from dotenv import dotenv_values
config = dotenv_values(".env")

supabase = Client(
    api_url=config.get("SUPABASE_URL"),
    api_key=config.get("SUPABASE_KEY")
)

async def main():
    # Insertion of Data

    error, result = await (
      supabase.table("posts")
      .insert([{"title": "post title"}])
    )

    # Updating of Data
    new_title  =  "updated title"
    _id        = 1
    error, result =  await (
      supabase.table("posts")
      .update(
        {"id"   : f"eq.{_id}"},
        {"title": new_title}
      )
    )

    # Deleting of Data

    error, result = await (
        supabase.table("posts")
        .delete({"id": _id})
    )

    # Filtering Data

    # All posts
    error, results = await (
        supabase.table("posts")
        .select("*")
        .query()
    )

    # Add limits/range
    error, results = await (
        supabase.table("posts")
        .select("*")
        .range(0,10)
        .query()
    )

    # Being specific
    error, results = await (
        supabase.table("posts")
        .select("*")
        .eq("id",1)
        .query()
    )
  
  
     

if __name__ == "__main__":
    loop = asyncio.get_event_loop()
    loop.run_until_complete(main())
```

## License
Supabase-Client is licensed under the [MIT License](https://mit-license.org/)

See [Supabase Docs](https://supabase.io/docs/guides/api)
