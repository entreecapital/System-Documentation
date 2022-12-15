# Building a workspace

Before you can use a workspace, you'll have to build it. To do so, switch to edit mode using the top-right "Edit layout" button.

### Managing components of your workspace <a href="#managing-components-of-your-workspace" id="managing-components-of-your-workspace"></a>

Components are the bricks of your workspace. To add a component, simply **drag & drop** it from the right-side component menu.

Naming your component can help you keep your workspace easy to understand and maintain. Components are given a default name upon creation, but this can be changed from the top-left of the settings panel of your component.

To delete a component, click on the ellipsis icon at the top-right of the settings panel of your component. In the dropdown, select "Delete component".

Deleting a component may impact other components. If this is the case, you'll be warned before proceeding.

### Understanding how components work <a href="#understanding-how-components-work" id="understanding-how-components-work"></a>

Write anything you wish to display, then customize how it's displayed using the style options.

Soon you'll be able to use markdown format as well.

The **Button** component can be used to trigger `global,` `single`, and `bulk` smart actions as well as CRUD operations.

If you've selected an action that requires selected record(s) to apply to, then you'll need to specify a source component:

Here we have linked the `action2` component so that when you select a record from the`collection1` component, you'll be able to trigger the _Edit a company_ action in 1 click.

The **Field** component lets you read data of a record that you selected in a "source" component.

**Source** components are components that let you select a record: Collection, Search, Dropdown components can be source components.

If you have a Collection component in your workspace, make sure its "On row click" option is set to "Select a record": this will allow you to select a record in your table, which in turn feeds the **Field** component.

In the Field component, select `collection1` as the source and choose which field value you wish to display: here we chose `name`.

You may have a more complex use case, where you'd want to display a property further away. To achieve this, you'll have to click the _Toggle to input code_ button:

For instance, if your collection is `Company` and it is linked to a `Country` collection, you may want to display `{{country.name}}` or even `{{country.headquarter.address}}`.

Note that you may also choose which [widget](broken-reference) to use to display your field.

The **(Inherited)** widget will use the same widget used in your Collection settings for this field.

Lastly you may also choose whether to display the label and customize it.

Use the Search component to quickly select a record within a given Collection:

With the above settings, you'll be searching within **all fields** of your `Company` records and displaying the [reference field](broken-reference).

The Search component can then be used in other components like Field ("on record from"), Text, (templating), Collection (templating in filter), Chart (templating in filter), etc.

The Dropdown is a great UI classic. Here's how you can set it up:

Choose a mode between "Static", "Dynamic > Simple" and "Dynamic > Smart"

In _Static_ mode, you hard-code values. You may re-order them using the handles.

_Enable search_ adds a search to your dropdown, making is easier to find values when there are many.

In _Simple_ mode, you choose a collection, a field and optionally a filter: this defines the values that will appear in the dropdown.

_Smart_ mode lets you fetch values from an external endpoint.

As explained in the tooltip, the expected response format is:

#### Making your components interact <a href="#making-your-components-interact" id="making-your-components-interact"></a>

Some of your components display data. You may want this data to influence other components. If you've read the [field component](broken-reference) section above, you've seen a simple way to make that happen. But there is another way: using **templating**. **Templating** is pseudo-code that will fetch the piece of data you want from a component. To start using it, simply type `{{` in a text input:

This opens an autocomplete dropdown which helps you use the correct syntax.

| Templating syntaxe                  | Result                                                       |
| ----------------------------------- | ------------------------------------------------------------ |
| `{{collection1.selectedRow.email}}` | Displays the column "email" of the select row of collection1 |
| `{{currentUser.fullName}}`          | Displays the current user's fullname                         |
| `{{currentUser.email}}`             | Displays the current user's email                            |
| `{{currentUser.team}}`              | Displays the current user's team                             |
| `{{currentUser.tags.some-tag}}`     | Displays the current user's value of the tag "some-tag"      |

If you rename your components, the syntax adjusts automatically in all components using templating.

Templating may also be used **in filters** of the Collection component. In practice, this allows you to recreate a Related data collection.

In the example above, we've set up collection1 (`Customer`) and collection2 (`Order`) so that when you click on a **Customer**, it shows **their Orders only** in collection2.

Templating is also useful within the **Chart** component: you may use other components' data to filter on your chart(s).

This feature is only available from version 9.0.0 for Express/Sequelize and Express/Mongoose and version 1.4.0 for agent-nodejs. If you're seeing this tooltip, you must upgrade first to benefit from the feature ​

For instance, if you want to display the number of fast boats belonging to a user, you may use a Collection component in combination with a "Single Value" chart with a filter set up as below:

Templating also works within **Query** mode, i.e within your SQL queries, like so:

**Bonus**: it's also possible to use templating in the Timeframe property of Time-based charts. This means that you could for instance create a **Dropdown** component with values _Day_, _Week_, _Month_ and _Year_ and using that dropdown would automatically refresh the chart based on the selected timeframe!

This is how you would set it up:
