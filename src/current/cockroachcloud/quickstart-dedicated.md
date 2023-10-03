---
title: Quickstart with CockroachDB Dedicated
summary: Learn how to create and use a CockroachDB Dedicated cluster.
toc: true
docs_area: get_started
---

This page shows you how to deploy a CockroachDB cluster on CockroachDB {{ site.data.products.dedicated }}, connect to it using a sample workload, and run your first query.

To run CockroachDB on your local machine instead, refer to [Start a Local Cluster](quickstart.html?filters=local).

## Step 1. Create a cluster

For this tutorial, you will create a 3-node GCP cluster in the `us-west2` region.

1. If you haven't already, <a href="https://cockroachlabs.cloud/signup?referralId=docs_quickstart_dedicated" rel="noopener" target="_blank">sign up for a CockroachDB {{ site.data.products.cloud }} account</a>.
1. [Log in](https://cockroachlabs.cloud/) to your CockroachDB {{ site.data.products.cloud }} account.
1. On the **Overview** page, click **Create Cluster**.
1. On the **Create Cluster** page, select **Dedicated standard**.
1. For **Cloud provider**, select **Google Cloud**.
1. For **Regions & nodes**, use the default selection of `California (us-west)` region and 3 nodes.

    {{site.data.alerts.callout_info}}
    To create a [multi-region]({% link cockroachcloud/plan-your-cluster.md %}#multi-region-clusters) cluster instead of a single-region cluster, select three regions and specify three nodes per region.
    {{site.data.alerts.end}}

1. Under **Hardware per node**, select 2vCPU for **Compute** and a 35 GiB disk for **Storage**.
1. Name the cluster. The cluster name must be 6-20 characters in length, and can include lowercase letters, numbers, and dashes (but no leading or trailing dashes).
1. Click **Next**.
1. On the **Summary** page, enter your credit card details.
1. Click **Create cluster**.

Your cluster will be created in approximately 20-30 minutes. Watch [this video](https://www.youtube.com/watch?v=XJZD1rorEQE) while you wait to get a preview of how you'll connect to your cluster.

Once your cluster is created, you will be redirected to the **Cluster Overview** page.

## Step 2. Create a SQL user

1. In the left navigation bar, click **SQL Users**.
1. Click **Add User**. The **Add User** dialog displays.
1. Enter a **Username** and **Password**.
1. Click **Save**.

## Step 3. Authorize your network

1. In the left navigation bar, click **Networking**.
1. Click **Add Network**. The **Add Network** dialog displays.
1. From the **Network** dropdown, select **Current Network** to auto-populate your local machine's IP address.
1. To allow the network to access the cluster's DB Console and to use the CockroachDB client to access the databases, select the **DB Console to monitor the cluster** and **CockroachDB Client to access the databases** checkboxes.
1. Click **Apply**.

## Step 4. Connect to your cluster

<section class="filter-content" markdown="1" data-scope="windows">
{{site.data.alerts.callout_success}}
[PowerShell](https://learn.microsoft.com/powershell/scripting/install/installing-powershell-on-windows) is required to complete these steps.
{{site.data.alerts.end}}
</section>

1. In the top-right corner of the Console, click the **Connect** button. The **Connect** dialog will display.
1. From the **SQL user** dropdown, select the SQL user you created in [Step 2. Create a SQL user](#step-2-create-a-sql-user).
1. Verify that the `us-west2 GCP` region and `defaultdb` database are selected.
1. Click **Next**. The **Connect** tab is displayed.
1. Select **Mac**, **Linux**, or **Windows** to adjust the commands used in the next steps accordingly.

    <div class="filters clearfix">
      <button class="filter-button page-level" data-scope="mac">Mac</button>
      <button class="filter-button page-level" data-scope="linux">Linux</button>
      <button class="filter-button page-level" data-scope="windows">Windows</button>
    </div>

1. {% include cockroachcloud/download-the-binary.md %}

1. In your terminal, run the second command from the dialog to create a new `certs` directory on your local machine and download the CA certificate to that directory.

    {% include cockroachcloud/download-the-cert.md %}

## Step 5. Use the built-in SQL client

1. In your terminal, run the connection string provided in the third step of the dialog to connect to CockroachDB's built-in SQL client. Your username and cluster name are pre-populated for you in the dialog.

    {{site.data.alerts.callout_danger}}
    This connection string contains your password, which will be provided only once. Save it in a secure place (e.g., in a password manager) to connect to your cluster in the future. If you forget your password, you can reset it by going to the **SQL Users** page for the cluster, found at `https://cockroachlabs.cloud/cluster/<CLUSTER ID>/users`.
    {{site.data.alerts.end}}

    {% include cockroachcloud/sql-connection-string.md %}

1. Enter the SQL user's password and hit enter.

    {% include cockroachcloud/postgresql-special-characters.md %}

    A welcome message displays:

    ~~~
    #
    # Welcome to the CockroachDB SQL shell.
    # All statements must be terminated by a semicolon.
    # To exit, type: \q.
    #
    ~~~

1. You can now run [CockroachDB SQL statements]({% link cockroachcloud/learn-cockroachdb-sql.md %}):

    {% include_cached copy-clipboard.html %}
    ~~~ sql
    > CREATE DATABASE bank;
    ~~~

    {% include_cached copy-clipboard.html %}
    ~~~ sql
    > CREATE TABLE bank.accounts (id INT PRIMARY KEY, balance DECIMAL);
    ~~~

    {% include_cached copy-clipboard.html %}
    ~~~ sql
    > INSERT INTO bank.accounts VALUES (1, 1000.50);
    ~~~

    {% include_cached copy-clipboard.html %}
    ~~~ sql
    > SELECT * FROM bank.accounts;
    ~~~

    ~~~
      id | balance
    -----+----------
       1 | 1000.50
    (1 row)
    ~~~

1. To exit the SQL shell:

    {% include_cached copy-clipboard.html %}
    ~~~ sql
    > \q
    ~~~

## What's next?

Learn more:

- Use the [built-in SQL client](https://www.cockroachlabs.com/docs/{{site.current_cloud_version}}/cockroach-sql) to connect to your cluster and [learn CockroachDB SQL]({% link cockroachcloud/learn-cockroachdb-sql.md %}).
- Build a ["Hello World" app with the Django framework](https://www.cockroachlabs.com/docs/{{site.current_cloud_version}}/build-a-python-app-with-cockroachdb-django), or [install a client driver](https://www.cockroachlabs.com/docs/{{site.current_cloud_version}}/install-client-drivers) for your favorite language.
- Use a local cluster to [explore CockroachDB capabilities like fault tolerance and automated repair](https://www.cockroachlabs.com/docs/{{site.current_cloud_version}}/demo-fault-tolerance-and-recovery).

Before you move into production:

- [Authorize the network]({% link cockroachcloud/connect-to-your-cluster.md %}#authorize-your-network) from which your app will access the cluster.
- Download the `ca.crt` file to every machine from which you want to [connect to the cluster]({% link cockroachcloud/connect-to-your-cluster.md %}#select-a-connection-method).
- Review the [production checklist]({% link cockroachcloud/production-checklist.md %}).