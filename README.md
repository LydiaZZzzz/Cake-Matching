# X Heal – ACL Recovery Assistant  
**Milestone 1 – Motion Classification with LSTM**

**Team 12** | Shangming Zhuo, Jazmyn Zhang, Yunqing Zhao, Auria Zhang  
**GitHub:** https://github.com/oivia123/515project

---

## Project Overview  
X Heal is a wearable system designed to help ACL patients perform rehabilitation exercises accurately at home.  
This milestone focuses on motion classification using sensor data from an MPU6050, enabling real-time feedback powered by machine learning.

---

## Data Collection & Labeling  
- Motion data was collected via a foot-mounted IMU (MPU6050)  
- Each 30-second session was manually labeled as one of three motion types:
  - `correct` – standard motion  
  - `err1` – side-to-side wobble  
  - `err2` – insufficient forward-backward swing  
- 5 CSV files were collected for each class

---

## Model Training  

### Data Processing  
- Normalized acceleration data (`ax`, `ay`, `az`) using training set  
- Applied a sliding window (length = 65, stride = 5) to generate fixed-size samples

### Model Architecture  
- LSTM(64) → Dense(64, relu) → Dense(3, softmax)  
- Loss function: `categorical_crossentropy`  
- Optimizer: `Adam (lr = 0.001)`

### Training Settings  
- Epochs: 20  
- Batch size: 32  
- One-hot encoded labels and shuffled training set  
- Final test accuracy: **100%**  
  > Due to the simplicity and clarity of the action categories

### Model Export  
- Saved in `.h5` format for future inference use

---

## Real-Time Demo Support  
We provide a Python script that loads the `.h5` model and predicts action type from any new CSV file containing motion data.  
The model returns the predicted label with confidence score.

---

## Files Included
- `train_model.py` – LSTM model training script  
- `demo_predict.py` – Prediction demo using new input data  
- `model/lstm_mpu_model.h5` – Trained model file  
- `data/*.csv` – Labeled motion datasets
