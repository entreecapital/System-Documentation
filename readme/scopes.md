# Scopes

A scope is a filter which applies to a collection and all its segments.

It is useful in that it can be used to control what data is available to users. More specifically, scopes can be set up to filter data dynamically on the current user.

**Scopes** are applied to the entire application excluding global smart actions, API & SQL charts and Collaboration & Activities.

Once on the Scopes tab **(1)**, you can set up your filter **(2)** and save **(3)**. In the above screenshot, only customers with an email ending with _@forestadmin.com_ will be displayed in the collection **and** all of its segments. All other customers won't be accessible.

Imagine a situation where you have several Operations teams each specialized in a specific country's operations:

* _France_ team handles customers from France
* _Germany_ team handles customers from Germany

If you set up the following scope...

...then Marc who belongs to the _France_ team will only see customers from France. However, Louis who belongs to the _Germany_ team will only see customers from Germany.

After the scope has been set up

In the example above, we used the team name to filter out what the user sees: `$currentUser.team.name`

Here the exhaustive list of available dynamic variables:

| Syntax                       | Result                                                                 |
| ---------------------------- | ---------------------------------------------------------------------- |
| `$currentUser.id`            | The id of the current user                                             |
| `$currentUser.firstName`     | The first name of the current user                                     |
| `$currentUser.lastName`      | The last name of the current user                                      |
| `$currentUser.fullName`      | The full name of the current user                                      |
| `$currentUser.email`         | The email of the current user                                          |
| `$currentUser.team.id`       | The id of the team of the current user                                 |
| `$currentUser.team.name`     | The name of the team of the current user                               |
| `$currentUser.tags.your-tag` | The value associated with key `your-tag` for the current user, if any. |

The above example is only possible if your data matches your users' details (email, team, etc). It's likely that it won't always be the case. This is why we've introduced user tags:

User tags are [set from each user's details page](<../.gitbook/assets/add and manage users>) and allow you to freely associate your users to a value which will match against your data using the `$currentUser.tags.your-tag` dynamic variable:

Using the above scope, the above user would see **1**, **2** but not **3**:
