# How to add or update a free course

The Learn page reads its list from `courses.json`. Edit that one file and the
live site updates for everyone. No HTML changes, no code changes, and visitors
who have used the site before still get the newest list.

## Adding a course

Open `courses.json` on GitHub, click the pencil icon, and add a block inside
`courses`. Copy an existing one and change the values:

```json
{
  "type": "cert",
  "provider": "HubSpot Academy",
  "title": "Social Media Marketing Certification",
  "niches": ["smm", "marketing"],
  "time": "medium",
  "timeLabel": "4 hrs",
  "gain": "One or two sentences on what they actually walk away with.",
  "link": "https://academy.hubspot.com/courses/social-media",
  "added": "2026-09-08"
}
```

Then change `"updated"` near the top of the file to today's date, and commit.
The site picks it up within seconds of the GitHub Pages build finishing.

## Field reference

| Field | What to put |
|---|---|
| `type` | `cert` = free certificate. `course` = good free learning, no certificate. `audit` = free to watch, certificate costs money. |
| `provider` | Who runs it, e.g. `Google`, `Meta`, `HubSpot Academy`, `Google / Coursera`. |
| `title` | The course name as the provider writes it. |
| `niches` | Any of: `ea`, `pm`, `smm`, `marketing`, `writing`, `design`, `video`, `tech`, `ecommerce`, `bookkeeping`, `cs`, `ai`. Use as many as genuinely apply. |
| `time` | `short` = under 2 hrs. `medium` = 2 to 10 hrs. `long` = 10 hrs or more. |
| `timeLabel` | What the visitor sees, e.g. `4 hrs`, `100+ hrs`. |
| `gain` | Why it is worth their time. Be specific and honest. |
| `link` | The direct enrolment URL. |
| `added` | Today's date as `YYYY-MM-DD`. |

## The NEW badge

Anything with an `added` date inside the last 30 days shows a lime **New**
badge automatically and sorts to the top of the list. After 30 days the badge
disappears on its own. Nothing to remember, nothing to clean up.

## Removing a course

Delete its block, or if you want to keep the details for later, move it to the
bottom of the file with a `"retired": true` field added. Retired entries are
ignored only if you delete them, so for now: delete the block.

## The weekly link check

Every Monday a GitHub Action opens each `link` and checks it still exists.
If anything is dead it opens an issue in this repository titled
"N course link(s) may be broken", listing each one. Open each link by hand to
confirm, because some providers block automated checks, then fix or remove the
entry in `courses.json`.

You can also run it any time: Actions tab, "Check course links", Run workflow.

## A note on fully automatic course feeds

There is no reliable free source that publishes "courses that are free right
now". Udemy closed its affiliate API on 1 January 2025, and Coursera and edX do
not offer an open feed. The unofficial coupon APIs that exist need a paid key,
and a static site like this cannot keep a key secret, since anything in the
page's JavaScript is visible to anyone who looks.

More importantly, the value of this page is that every entry has been checked
by a person. Auto-publishing unvetted coupon courses would fill it with
expiring links and weaken exactly what makes it worth visiting.

So the automation here is deliberately split: adding a course is one small edit
in one file, and keeping the list honest is handled by the weekly link check.
