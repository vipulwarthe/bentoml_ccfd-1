# Deploy ml Model to detect credit card fraud detection with Bentoml
git clone https://github.com/Devendra61/bentoml_ccfd.git
cd bentoml_ccfd
pip install -r requirements.txt
python3 train.py
bentoml serve service:svc --reload
# (open the port 8080 with instance ip)
