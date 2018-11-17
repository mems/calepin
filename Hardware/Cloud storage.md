Note: Can't backup to Amazon Glacier with Hyper Backup, require to use Glacier Backup app

Backup 2TB of data with NAS (Synology - Hyper Backup):

For total of 3TB per year (TTC):

- Amazon Drive 299,97€
- Dropbox Business Advanced 648€ (3 users minimum, unlimited storage)
- Synology C2 209,97€ only from Synology NAS with DSM
- Amazon Glacier 144$ HT + 0.055/1000 write op (only available via Glacier Backup app)
- Amazon S3 RRS 450$ HT
- Microsoft Azure Blob Storage, LRS Cool, West Europe 306€ +0.0844/10000 write op
- Microsoft Azure Blob Storage, LRS Archive, West Europe 61,2€ +0.0844/10000 write op (not supported)
- Google Storage Coldline 211,743€ (compatible S3)
- Blackbaze B2, 100GB/m upload, 10GB/m delete, 0GB download 215$ (only available via Cloud Sync)
- Wasabi, $143 (compatible S3)

For total of 4TB per year:

- Amazon Drive 399,96€
- Dropbox Business Advanced 648€ (3 users minimum, unlimited storage)
- Synology C2 279,96€ only from Synology NAS with DSM
- Amazon Glacier 192$ HT + 0.055/1000 write op (only available with Glacier Backup app)
- Amazon S3 RRS 600$ HT
- Microsoft Azure Blob Storage, LRS Cool, West Europe 408€ +0.0844/10000 write op
- Microsoft Azure Blob Storage, LRS Archive, West Europe 81,6€ +0.0844/10000 write op (not supported)
- Google Storage Coldline 282,324€ (compatible S3)
- Blackbaze B2, 100GB/m upload, 10GB/m delete, 0GB download 275$ (only available via Cloud Sync)
- Wasabi, $191 (compatible S3)

[With CrashPlan getting out of the consumer cloud backup game, what’s next best? - Ars Technica OpenForum](https://arstechnica.com/civis/viewtopic.php?p=33882005&sid=8da3f27339eda23101933e8014e690b9#p33882005)

S3 proxy to Blackbaze B2 https://github.com/gaul/s3proxy (Java in a Docker image)

- [Cloud Storage | Object Storage | Hot Storage | Wasabi Technologies](https://wasabi.com/) `$0 = document.querySelector(".fc__calc_range_slider");$0.value = 3;$0.dispatchEvent(new InputEvent("change"));`
- [Cloud Storage Providers: How Much Do They Really Charge?](https://www.backblaze.com/blog/transparency-in-cloud-storage-costs/) (calculator doesn't work on Chrome and Firefox?)
- [Tarifs de Dropbox Business - Dropbox Business](https://www.dropbox.com/business/pricing)
- [Tarification du stockage dans le cloud – Amazon Simple Storage Service (S3) – AWS](https://aws.amazon.com/fr/s3/pricing/)
- [Tarification du stockage d'archives dans le cloud – Amazon Glacier – AWS](https://aws.amazon.com/fr/glacier/pricing/)
- [Synology C2](https://c2.synology.com/fr-fr/backup#tab_plan)
- [Manage Storage](https://www.amazon.fr/clouddrive/managestoragev2/allPlans?mgh=1) [Amazon.com: : Pricing FAQ](https://www.amazon.com/b?node=16591160011)
- [Azure Storage Blobs Pricing | Microsoft Azure](https://azure.microsoft.com/en-us/pricing/details/storage/blobs/)
- [Tarifs de Cloud Storage | Cloud Storage Documentation | Google Cloud Platform](https://cloud.google.com/storage/pricing#storage-pricing)
- [SKUs | Google Cloud Platform](https://cloud.google.com/skus/?currency=EUR&filter=Coldline)
- Wasabi [Cloud Storage | Object Storage | Hot Storage | Wasabi Technologies](https://wasabi.com/)
	`https://s3.wasabisys.com`
	- [Wasabi Technologies, Inc | Crunchbase](https://www.crunchbase.com/organization/wasabi-technologies-inc#section-overview)
	- [Wasabi, Founded By Ex-Carbonite Team, Plans To Attack S3 Storage Market With Disruptive Price, Performance](https://www.crn.com/news/storage/300084774/wasabi-founded-by-ex-carbonite-team-plans-to-attack-s3-storage-market-with-disruptive-price-performance.htm)

- [Cloud Backup - Prizes and Thoughts Addendum: Synology, Software, Wasabi](https://translate.google.com/translate?sl=auto&tl=en&js=y&prev=_t&hl=en&ie=UTF-8&u=https%3A%2F%2Fwww.nsonic.de%2Fblog%2F2018%2F01%2Fcloud-backup-preise-und-gedanken-nachtrag-synology-software-wasabi%2F&edit-text=&act=url) - Backup synology to Wasabi (and how retrive backup without DiskStation: mount S3 and use Hyper Backup Explorer)
- [Backblaze B2 Reaching "Class C Transactions Cap" with Synology NAS - Daniel Gibbs](https://danielgibbs.co.uk/2016/08/b2-class-c-transaction-caps-synology/)
- [How do I use Synology with Wasabi? – Wasabi Knowledge Base](https://wasabi-support.zendesk.com/hc/en-us/articles/115001684131-How-do-I-use-Synology-with-Wasabi-)
- [Azure Archive Storage with Hyper Backup? : synology](https://www.reddit.com/r/synology/comments/7gjxmb/azure_archive_storage_with_hyper_backup/)
- [Destination | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/help/HyperBackup/data_backup_destination)
- [Glacier Backup | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/help/GlacierBackup/help)
- [Back up your synology NAS data in Windows Azure Cool Storage – Paris Polyzos' blog](https://ppolyzos.com/2016/05/07/back-up-your-synology-nas-data-in-windows-azure-cool-storage/)
- [Synology NAS to Glacier Backup - The Ultimate Guide -](https://www.ceos3c.com/2017/07/28/synology-nas-glacier-backup-ultimate-guide/)
- [Amazon Glacier Backup : Sauvegarde d'un NAS Synology](http://blog.e-nnov.fr/synology-dsm/glacier/#.WlKJloJG3UI)
- [Amazon Glacier - Anyone Using It? - Page 2 - Synology Forum](https://forum.synology.com/enu/viewtopic.php?f=228&t=79270&start=15)
- [Cloud Storage Interoperability | Cloud Storage Documentation | Google Cloud Platform](https://cloud.google.com/storage/docs/interoperability) - "The Google Cloud Storage XML API is interoperable with some cloud storage tools and libraries that work with services such as Amazon Simple Storage Service (Amazon S3)"
