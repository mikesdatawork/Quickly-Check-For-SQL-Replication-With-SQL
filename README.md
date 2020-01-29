![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# Quickly Check For SQL Replication With SQL
**Post Date: October 16, 2017**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>Want to quickly check to see if your Database Server has Replication configured? Try this little bit of SQL Logic.

![Use SQL To Check For Replication]( https://mikesdatawork.files.wordpress.com/2017/10/check_for_replication.png?w=829 "Check For Replication")</p>    

  
## SQL-Logic
```SQL
use master;
set nocount on
 
-- check if database server has replication configured at all
 
select
     'sql_instance'     = upper(@@servername)
,    'has_replication'  = case when sum(cast(sd.is_published as int) + cast(sd.is_subscribed as int)) > 0 then 'Yes' else 'No' end
from
    sys.databases sd
 
-- check which databases are involved in replication
select
    'database'      = upper(sd.name)
,   'published'     = case sd.is_published      when 0 then 'no' else 'yes' end
,   'published_merge'   = case sd.is_merge_published    when 0 then 'no' else 'yes' end
,   'distributor'   = case sd.is_distributor    when 0 then 'no' else 'yes' end
,   'subscriber'    = case sd.is_subscribed     when 0 then 'no' else 'yes' end
from
    sys.databases sd
where
    database_id > 4
order by sd.name asc
```


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

     
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

