# Private Production of VLL UL samples

**Models:** VLL(Doublet) and VLL(Singlet)

**Coupling:** VLL-e like, VLL-mu like and VLL-tau like

**Mass**
- 100 GeV to 1200 GeV( for doublet)
- 100 GeV to 1000 GeV( for singlet)

**Campaign**
- 2016PreVFP: RunIISummer20UL16
- 2018PostVFP: RunIISummer20UL16APV
- 2017: RunIISummer20UL17
- 2018: RunIISummer20UL18

Resource:
- EXO gitbook: https://exo-mc-and-i.gitbook.io/exo-mc-and-interpretation/how-to-sample-production-private
- Gridpack: https://twiki.cern.ch/twiki/bin/view/CMS/QuickGuideMadGraph5aMCatNLO
- PdMV: https://twiki.cern.ch/twiki/bin/view/CMS/PdmV

- Chain Request for Sample Production: https://cms-pdmv.cern.ch/mcm/requests?prepid=EXO-RunIISummer20UL18DIGIPremix-01534&page=0&shown=127 

# Production Steps

```
gridpacks generation >>> LHEGS >>> Premix >> AODSIM >> MINIAODSIM >> NANOAODSIM

```
1. **gridpacks:** Bunch of necessary files in a tar file to produce LHE events from the model UFO. We can change the model parameter, mass of the VLLs while producing gridpacks and facilitate the LHE events generation. The output of this step is gridpacks which is a tarball containing InputCards,MadGraph stuffs etc. *Gridpacks contain all the information of process that will be generated and simulated at subsequent steps.*

2. **LHEGS:** It takes the gridpacks and produce LHE-->GEN-->SIM events.

3. **PreMix:** It takes SIM events-->DIGI,DATAMIX,L1,DIGI2RAW,HLT

4. **AODSIM:** Physics objects (e.g. muons, jets, etc.) are reconstructed. The output format of this step is generally in AODSIM format (RAW2DIGI,L1Reco,RECO,RECOSIM). This is also called RECO step.

5. **MiniAOD:** From AOD to MiniAOD

6. **NanoAOD:** From MiniAOD to NanoAOD

NB:
- LHEGS step can be splitted in LHE-GEN and SIM step separately
- Premix step can be splitted in DIGIPremix and HLT separately

## Instructions

1. Gridpack generation

## LHEGS step

For UL settings, do the following,

```
>>> export SCRAM_ARCH=slc7_amd64_gcc700

>>> cmsrel CMSSW_10_6_30_patch1

# Download fragment from McM
>>> curl -s -k https://cms-pdmv.cern.ch/mcm/public/restapi/requests/get_fragment/EXO-RunIISummer20UL18wmLHEGEN-01288 --retry 3 --create-dirs -o Configuration/GenProduction/python/EXO-RunIISummer20UL18wmLHEGEN-01288-fragment.py

>>> scram b

>>>cmsDriver.py Configuration/GenProduction/python/EXO-RunIISummer20UL18wmLHEGEN-01288-fragment.py --python_filename EXO-RunIISummer20UL18wmLHEGEN-01288_1_cfg.py --eventcontent RAWSIM,LHE --customise Configuration/DataProcessing/Utils.addMonitoring --datatier GEN,LHE --fileout file:EXO-RunIISummer20UL18wmLHEGEN-01288.root --conditions 106X_upgrade2018_realistic_v4 --beamspot Realistic25ns13TeVEarly2018Collision --step LHE,GEN --geometry DB:Extended --era Run2_2018 --no_exec --mc -n 10

setup link:https://cms-pdmv.cern.ch/mcm/public/restapi/requests/get_setup/EXO-RunIISummer20UL18wmLHEGEN-01288
```

##

