## hb-appstore meta-repo
This repo is served at [fortheusers.github.io/meta-repo](https://fortheusers.github.io/meta-repo/index.json) with a backup [meta.fortheusers.org](https://meta.fortheusers.org/index.json), in case the primary meta-repo URL is down or can't be reached.

It serves as an index of suggested actions for the [hb-appstore](https://github.com/fortheusers/hb-appstore) client to take, in terms of managing its [libget](https://github.com/fortheusers/libget) repos.

For example, some legacy users have local repo config files that still point to the non-CDN servers. Versions of hb-appstore 2.4 and up reference this meta-repo to see if there are any known repos that need their URLs updated. This can also be helpful if new repos are added (for example of some packages are split up) or some old repo URLs go down and need to be changed.

### Format
The top level contains a "suggestions" key, which provides a list of potential operations that the client can take. Each key within that object represents the platform that the operations should apply to. The operations will only run on clients that match the platform.

There are some circumstances where a client may match multiple platforms, such as the Wii U checking both "wiiu" and "vwii". For a full list, see hb-appstore's codebase. (TODO)
```
{
    "suggestions": {
        "wiiu": [ Operation1, Operation2, ... ],
        "switch": [ Operation1, Operation2, ... ],
        "vwii": [ Operation1, Operation2, ... ],
        "wii": [ Operation1, Operation2, ... ],
        "3ds": [ Operation1, Operation2, ... ]
    }
}
```

The different operations are detailed below.

#### "add"
Append a repo with `url` of `type`, if this URL doesn't exist already. If it does exist, but is a different type, it will be changed to the `type`.
```
{
    "op": "add",
    "url": "https://cdn.newval.com",
    "type": "get"
}
```

#### "remove"
Remove the `url` from the list of repos, if it exists. If no repos remain after the removal occurs, the client will regenerate the repo list with the default 
```
{
    "op": "remove",
    "url": "https://oldurl.com"
}
```

#### "exclude"
Excludes and hides the given `pkgName` from any repos that it might appear in. At this time, this will exclude it from any repos that match the name.
```
{
    "op": "exclude",
    "pkgName": "name-of-package"
}
```
