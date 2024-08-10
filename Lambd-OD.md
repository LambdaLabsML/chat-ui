# Deploy on Lambda Cloud On-Demand Instance

From Lambda on-demand instance:
```bash
# Launch mongoDB
export USERNAME=$(whoami) && \
sudo usermod -aG docker $USERNAME && \
newgrp docker && \
docker run -d -p 27017:27017 --name mongo-chatui mongo:latest

# Install npm
sudo apt install npm
sudo npm install -g n
sudo n stable
export PATH="$HOME/n/bin:$PATH"

# Update API_KEY & model config in .env 
# Currently model config is set to use a opensource model (OpenAI API compatible) hosted behnind Lambda auth proxy
# To use this model, set OPENAI_API_KEY in .env to a valid Lambda cloud api key

# Launch chat-ui
git clone https://github.com/huggingface/chat-ui
cd chat-ui
npm install
npm run dev -- --open
```

From your local machine:
```bash
# Port forwarding
ssh -i ~/.ssh/ml.pem -L 5173:localhost:5173 ubuntu@<hosting-server-ip>

# Visit chat-ui at 
http://localhost:5173/
```
