# RingCounting

The RingCounting Tool is used to classify events into single- and multi-Cherenkov-ring-events.
For this a CNN-based machine learning approach is used. 
---
This Tool uses PMT data in the CNNImage format (see UserTools/CNNImage). For further details on the tool and
the models used (including performance etc.) see the documentation found on the anniegpvm-machines at (**Todo**)
```
/pnfs/annie/persistent/reconstruction/RingCounting/RingCountingStore/documentation/
``` 

---

All models can be found at
```
/pnfs/annie/persistent/reconstruction/RingCounting/RingCountingStore/models/
```
---
## Data

- In the "load_from_file" mode, this tool adds single- and multi-ring (SR/MR) predictions to the RecoEvent BoostStore. When theh "load_from_file" config parameter is set to 0, the tool instead outputs the predictions to a csv file.
- The predictions are stored in the "RingCountingSRPrediction" and "RingCountingMRPrediction" variables 

The predictions are given as probabilities in the interval [0,1] as doubles, and sum to 1 for both classes.

Implemented as:
```
reco_event_bs = self.m_data.Stores.at("RecoEvent")

reco_event_bs.Set("RingCountingSRPrediction", predicted_sr)
reco_event_bs.Set("RingCountingMRPrediction", predicted_mr)
```

---
## Configuration

The following configuration variables must be set for the tool to function properly.

---
Exemplary configuration:
```
PythonScript RingCounting

InitialiseFunction Initialise
ExecuteFunction Execute
FinaliseFunction Finalise

verbose 1

# analysis specific settings
#
# Define file containing (multiple) filepath(s) to be loaded
load_from_file 0
files_to_load configfiles/RingCounting/files_to_load.txt
# Model version -> check documentation
version 1_0_0
# Folder containing models
model_path /exp/annie/app/users/dschmid/RingCountingStore/models/
# Masked PMTs (to 0) config -> check documentation
pmt_mask november_22
# Output file
save_to RC_output.csv
```
