+++
Categories = ["console"]
Description = ""
Tags = ["console"]
date = "2016-08-10T09:21:22+12:00"
menu = "main"
title = "Navigating Less"

+++

Several git commands, such as `git log`, bring you into the Unix Less program. This looks like the following:

```text
commit 3abb211726b175b326afade16adc79876dfc3905
Author: Regan Ryan <regan.ryan@email.com>
Date:   Tue Aug 9 16:38:20 2016 +1200

    added super admin buttons to act/deactivate account

commit 396a65574144f880b12b351ea319fb1300f4e81a
Author: Regan Ryan <regan.ryan@email.com>
Date:   Tue Aug 9 14:45:12 2016 +1200

    making admin partials (to be unified with publisher partials)

commit 8cafcbf8e3ca864ed2f37ce4ea8f4cdf85238951
Author: Regan Ryan <regan.ryan@email.com>
Date:   Tue Aug 9 13:11:41 2016 +1200

    added account fields to active pub (admin view)

commit 9709e2c1819cb5c23aa77fb832beefb2f98e5672
Merge: 6d31bd4 44e3c2a
Author: ReganRyanNZ <regan.ryan@email.com>
Date:   Tue Aug 9 14:43:40 2016 +1200

    Merge pull request #75 from ReganRyanNZ/sf-colordefaults

:
```

The `:` at the end indicates your are inside Less. Here are some basic commands to help navigate:

- `q` quits out of Less.
- `j` next line.
- `k` previous line.
- `f` forward one screenful.
- `b` back one screenful.
- `/` type in a phrase and press `Enter` to search.
  - `n` find next.
  - `N` find previous.