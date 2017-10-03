---
title: users.lua
keywords: authentication
sidebar: userguide_sidebar
permalink: userguide_users.html
folder: userguide
toc: false
---

Defines the valid authentication the server will require when streams are pushed into the EMS.

Where:

- user1 = name of first user
- user2 - name of second user
- password1 = password of the first user
- password2 = password of the second user

```
users=
{
	user1="password1",
	user2="password2",
}

realms=
{
	{
		name="EVOSTREAM stream router",
		method="Digest",
		users={
			"user1",
			"user2",
		},
	},
}
```

------

##Notes:

- You may add or delete number of users in this file
- Authentication (auth.xml) should be enabled to use this file


------

## Related Links

- [auth.xml](/userguide_auth.html)