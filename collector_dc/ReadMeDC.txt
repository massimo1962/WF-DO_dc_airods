
---------

collector for dublin core wf catalog 

---------
how it works:
this script get info from irods icat catalog (pid) and info retrieved from station fdsn ws (lat,lon) and insert, along with other dc values extracted from files, into mongo collection; in the same db used in EIDA or another.  

configuration:
fill config2.json, it is very similar to the 'EIDA' one.
Be aware to put the rigth cls_orm value, this field is needed for orm mongo class used in http-api-airods, 
the current value is "b2stage.models.mongo.wf_do".
Btw in the header of WFCatalogCollector-dc.py all value are descripted in somehow.
The script need the same environment (python) used for EIDA WF-Catalog. 
The MongoDb could be different from EIDA 

run:
python WFCatalogCollector-dc.py --dir datastore/2015/IV/ --dc_on  --logfile /data/ingestion_one.log

note:
It is possible launch the Collector via docker container builded on Dockerfile stored into dir build/ (the same used in EIDA) in order to use this script everywhere.

build:
sudo docker build -t "wfcatalog-collector:1.0" .

run docker interactive:
sudo docker run -ti -v /home/user/store/archive:/usr/src/collector/datastore -v /home/user/wfcatalog-dc/collector_dc:/usr/src/collector --name collector_wfcat  wfcatalog-collector:1.0

run like executable: 
sudo docker run -ti -v /home/user/store/archive:/usr/src/collector/datastore -v /home/user/wfcatalog-dc/collector_dc:/usr/src/collector --name collector_wfcat  wfcatalog-collector:1.0 python /usr/src/collector/WFCatalogCollector-dc.py --dir datastore/2015/IV/ --dc_on  --logfile /data/ingestion_dc.log






