# Segments

A Segment is a subset of a collection gathering filtered records.

Segments are designed for those who want to _systematically_ visualize data according to specific sets of filters. It allows you to save your filters configuration so you don’t have to compute the same actions every day (e.g. signup this week, pending transactions).

Forest Admin provides a straightforward UI to configure the segments you want step-by-step. The only information Forest Admin needs to create a segment within a collection is a name and some filters.

To create a new segment, activate the Layout Editor mode **(1)** on the top right part of your screen and click on the cog just next to the collection you want to edit **(2)** and select the _Segments_ tab **(3).**

At this point there are 2 possibilities:

If you have never created any segment for this collection, click the "Create your first segment" **(4)**.

Otherwise, click the "+ New segment" link **(5)**.

To create your segment, give it a name **(6)** and add 1 or more filter(s) **(7)**. You can also adjust your **sorting** **field** and **order** [like you would for a collection](broken-reference).

#### Create SQL Query Segments <a href="#create-sql-query-segments" id="create-sql-query-segments"></a>

Forest Admin gives you a second option to create segment: SQL queries.

**Query** **mode** is only available for databases which support SQL. For **security** reasons, only `SELECT` queries are allowed.

SQL queries allow you to create advanced filters and connect your data through a few lines of code if you know how SQL queries work.

Simply switch to **Query** mode **(1)**, type in your SQL query **(2)** and save.

SELECT t.id FROM transactions t

JOIN companies beneficiary ON t.beneficiary\_company\_id = beneficiary.id

JOIN companies emitter ON t.emitter\_company\_id = emitter.id

WHERE beneficiary.headquarter ILIKE '%United States%' AND emitter.headquarter ILIKE '%United States%'

The returned column **must** be `id` .

In the above example, we display the transactions whose beneficiaries and emitters are in the United States.

If you want to make a SQL segment based on several databases, you can use the [dblink function](https://www.postgresql.org/docs/10/contrib-dblink-function.html) for postgreSQL.

#### Organize your workflows through with the layout editor ​ <a href="#organize-your-workflows-through-with-the-layout-editor" id="organize-your-workflows-through-with-the-layout-editor"></a>

Usually, you want the organization of your segments to match the sequencing of your business workflows. To do so, you can **reorder** your segments using the Layout Editor mode just [like you would for collections](<../.gitbook/assets/using the layout editor mode>).

By default, newly created segments are **disabled**.
