{{ site.data.products.db }} support two types of backups:

- **Managed-service backups**: Cockroach Labs takes automated backups of {{ site.data.products.serverless }} and {{ site.data.products.dedicated }} clusters that are stored in Cockroach Labs' cloud storage. {% if page.name != "use-managed-service-backups.md" %} See [Use Managed-Service Backups](../cockroachcloud/use-managed-service-backups.html) to learn more about the type and frequency of backups supported for both {{ site.data.products.db }} clusters. {% else %}  {% endif %}
- {% if page.name == "take-and-restore-customer-owned-backups.md" %} **Customer-owned backups**: {% else %} **[Customer-owned backups](../cockroachcloud/take-and-restore-customer-owned-backups.html)**: {% endif %} You can take manual backups and store them in your [cloud storage buckets](../{{site.versions["stable"]}}/use-cloud-storage.html) using the [`BACKUP`](../{{site.versions["stable"]}}/backup.html) statement. 