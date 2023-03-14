# botnet-detection
The prototype for network flow-based botnet detection using AI models.

## Files
- `playbook.ipynb` - basic demo on how to use the model and estimate its accuracy on the given data.
- `adversarial.ipynb` - a prototype trying to generate adversarial the samples from the malicious ones
- `dnn_2epochs.h5` - Pretrained DNN model. 72 inputs, 16x16x16 dense layers (act. ReLU), 1 output (act. sigmoid).
- `scaler.pkl` - [sklearn.preprocessing.MinMaxScaler](sklearn.preprocessing.MinMaxScaler) fited during training.
- `/flows`
  - `Selected_Flows.csv` - 401 MALICIOUS flows with prediction confidense >90%. Used for adversarial samples generation simulation in `adversarial.ipynb` 
  - `/examples` - several cherry-picked malicious flows with their corresponding PCAP dumps.

## Data
- Original UNB CIC **Botnet 2014** (PCAP dumps + IP labels): https://www.unb.ca/cic/datasets/botnet.html
- Obtained network flows (CSV, labeled)
    - Training: **ISCX_Botnet-Training.pcap_Flow.csv** (~220MB) https://bit.ly/3JgelUy
    - Testing: **ISCX_Botnet-Testing.pcap_Flow.csv** (~165MB) http://bit.ly/42dUn5x

### Flows features
- Identification fields: *Src IP, Src Port, Dst IP,Dst Port, Protocol,Timestamp*
- Features: *Flow Duration, Fwd/Bwd Header Length,
(Fwd/Bwd) Packet Length Min/Max/Mean/Std/Total, Total Fwd/Bwd Packets, (Fwd/Bwd) Inter-
Arrival Time Min/Max/Mean/Std/Total, (Fwd/Bwd) SYN/FIN/ACK/RST/CWR/PSH/URG/ECE flags
count, Packets/second, Bytes/second, Flow Active Duration Min/Max/Mean/Std, Subflow (Fwd/Bwd)
Packets/Bytes, Up/Down Ratio*
- Label: *FlowType* (should be mapped to 0 - BENIGN or 1 - MALICIOUS)
- Other: *FlowTerminationReason, HostType, Predicted Probability, Predicted Type*

## Tools
- **CICFlowmeter-V4.0** - used (with minor adjustments) to compute flow features and store them as CSV from PCAPs. https://github.com/ahlashkari/CICFlowMeter