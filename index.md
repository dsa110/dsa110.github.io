# DSA-110 Software Status


## Web services
Tunnel to dsa-storage:
|
[Web UI](http://localhost:9090)
|
[Grafana](http://localhost:3000)
|
[Antenna/BEB status](http://localhost:5006)
|
[Candidate Hiplot](http://localhost:5007/?hip.load_uri=%22<set date string>%2Fcluster_output.csv%22&hip.filters=%5B%5D&hip.color_by=%22snr%22&hip.PARALLEL_PLOT.order=%5B%22dm%22%2C%22ibeam%22%2C%22ibox%22%2C%22mjds%22%2C%22snr%22%2C%22trigger%22%5D&hip.PARALLEL_PLOT.hide=%5B%22cl%22%2C%22cntb%22%2C%22cntc%22%2C%22idm%22%2C%22if%22%2C%22itime%22%5D&hip.XY.axis_y=%22dm%22&hip.XY.axis_x=%22mjds%22&hip.params.ibox.type=%22numericlog%22&hip.PARALLEL_PLOT.invert=%5B%5D)
|
[Jupyter server](http://localhost:8900)
|
![test](maas.jpg) [MAAS](http://localhost:5240)

Real-time processes [diagram](https://caltech.sharepoint.com/sites/ovro/projects/dsa110observerwiki/Start%20digital%20and%20search%20pipeline.aspx):

Task | Script/Cnf | Where | How to Run | Input | Output | Repo
---- | ------ | ------| ---------- | ----- | ------ | ----
F-engine | [snap.py](https://github.com/dsa110/SNAP_control/blob/master/scripts/snap.py) | SNAPs 00--07 | snapservice, `/cmd/snap` | -- | corr01--corr16 | [SNAP_control](https://github.com/dsa110/SNAP_control)
Correlator/BF  | [corr cnf](https://github.com/dsa110/dsa110-cnf/blob/master/config_corr_nodes.yaml) | corr 01--16  | `/cmd/corr`, `dsacon corr start/set/stop` | F-engine | calibration, heimdall | [dsa110-xengine](https://github.com/dsa110/dsa110-xengine) (also controls [dsa110-meridian-fs](https://github.com/dsa110/dsa110-meridian-fs))
Heimdall (T1) | [search cnf](https://github.com/dsa110/dsa110-cnf/blob/master/config_search_nodes.yaml) | corr17--20 | `/cmd/corr`, `dsacon corr start/stop` | BF | T2 | [dsa110-mbheimdall](https://github.com/dsa110/dsa110-mbheimdall)
T2 | `run_T2.py` | corr00 | screen session "T2" | Heimdall | voltage trigger (via etcd) | [dsa110-T2](https://github.com/dsa110/dsa110-T2)
Calibration | [preprocess_service.py](https://github.com/dsa110/dsa110-calib/blob/main/services/preprocess_service.py), [calibration_service.py](https://github.com/dsa110/dsa110-calib/blob/main/services/calibration_service.py), beamformerweights.py | dsa-storage | /cmd/cal, /mon/cal/bfweights | correlator | bf weights | [dsa110-calib](https://github.com/dsa110/dsa110-calib)
T3 slack | [send_cands.py](https://github.com/dsa110/dsa110-T3/blob/main/services/send_cands.py) | h23 | user service | filterbank files | candidate plot | [dsa110-T3](https://github.com/dsa110/dsa110-T3)
bbproc? | ? | dsa-storage | ? | volage buffer | candidate plots | [dsa110-bbproc](https://github.com/dsa110/dsa110-bbproc)

## Code Tests and Docs

[Issues](https://github.com/dsa110/dsa110-issues)
|
[Calibration](https://dsa110.github.io/dsa110-calib/) [![dsa110-calib](https://travis-ci.com/dsa110/dsa110-calib.svg?branch=main)](https://travis-ci.com/dsa110/dsa110-meridian-fs.svg?branch=main)
|
[T2](https://dsa110.github.io/dsa110-T2/) [![dsa110-T2](https://travis-ci.com/dsa110/dsa110-T2.svg?branch=master)](https://travis-ci.com/dsa110/dsa110-T2)
|
[antpos](https://github.com/dsa110/dsa110-antpos) [![dsa110-antpos](https://travis-ci.com/dsa110/dsa110-antpos.svg?branch=master)](https://travis-ci.com/dsa110/dsa110-antpos)
|
[fringe stopping](https://github.com/dsa110/dsa110-meridian-fs) [![ds110-meridian-fs](https://travis-ci.com/dsa110/dsa110-meridian-fs.svg?branch=main)](https://travis-ci.com/dsa110/dsa110-meridian-fs.svg?branch=main)


## Repo Links

**Hardware**
|
[DSA antpos](https://github.com/dsa110/dsa110-antpos)
|
[Antenna alignment](https://github.com/dsa110/dsa110-alignment)


**Digital**
|
[SNAP control](https://github.com/dsa110/SNAP_control/tree/v3)
|
[SNAP power](https://github.com/dsa110/dsa110-powersnap)
|
[X engine](https://github.com/dsa110/dsa110-xengine)


**Calibration**
|
[Fringe stopping](https://github.com/dsa110/dsa110-meridian-fs)
|
[Calibration](https://github.com/dsa110/dsa110-calib)
|
[Calibration tools](https://github.com/dsa110/dsa110-caltools)


**Search**
|
[MB Heimdall](https://github.com/dsa110/dsa110-mbheimdall)
|
[T2](https://dsa110.github.io/dsa110-T2/)


**Analysis and Data Management**
|
[Analysis notebooks](https://github.com/dsa110/dsa-notebooks)
|
[bbproc](https://github.com/dsa110/dsa110-bbproc)
|
[procfil](https://github.com/dsa110/dsa110-procfil)
|
[scripts](https://github.com/dsa110/dsa110-xengine/tree/v0.9/scripts) (scripts to be reorganized)


**M&C**
|
[M&C and utilities](https://github.com/dsa110/dsa110-pyutils)
|
[DSA hardware M&C](https://github.com/dsa110/dsa110-hwmc)
|
[Antenna status (bokeh)](https://github.com/dsa110/dsa110-vis)
