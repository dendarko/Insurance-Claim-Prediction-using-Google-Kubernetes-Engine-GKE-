
# Insurance Claim Prediction Pipeline Deployment on Google Kubernetes Engine (GKE)

## Project Overview

This project showcases the deployment of a machine learning pipeline on **Google Kubernetes Engine (GKE)** for predicting insurance claims. The pipeline involves the following key steps:

- Data preprocessing and model training using **PyCaret**.
- Building a **Flask** API to expose the model for predictions.
- Containerizing the application using **Docker**.
- Deploying the containerized app to **Google Kubernetes Engine** (GKE).
  
The model predicts whether an insurance claim is likely to occur based on customer demographics, vehicle details, and insurance-related features.

## Key Technologies

- **Google Kubernetes Engine (GKE)** for managing the deployment of containerized applications.
- **Flask** for creating a REST API to serve the model.
- **Docker** for containerizing the application.
- **PyCaret** for machine learning model development.
- **Google Cloud Platform (GCP)** for cloud infrastructure.
- **Python** for scripting and model development.

## Project Structure

Here’s an overview of the main files and directories in the project:

- **\`Dockerfile\`**: Defines instructions for building the Docker image of the Flask app.
- **\`app.py\`**: Contains the Flask API with endpoints for model predictions.
- **\`config.py\`**: Configuration settings for the Flask application.
- **\`deployment_28042020.pkl\`**: The saved PyCaret machine learning model used for predictions.
- **\`requirements.txt\`**: Lists the dependencies required for the project.
- **\`templates/home.html\`**: HTML file for the web interface.
- **\`static/style.css\`**: CSS file for styling the web interface.
- **\`Insurance - Model Training Notebook.ipynb\`**: Jupyter notebook for training the model.
- **\`.gcloudignore\`**: Specifies files to be ignored when deploying to Google Cloud.

## Workflow

### 1. Model Development and Training
The Jupyter notebook (\`Insurance - Model Training Notebook.ipynb\`) contains the steps for data preprocessing and model training using PyCaret. The trained model is saved as a \`.pkl\` file (\`deployment_28042020.pkl\`) for later deployment.

### 2. Flask API
The \`app.py\` file contains the **Flask** application that exposes the trained model through a \`/predict\` endpoint. The API accepts input data in JSON format and returns a prediction based on the trained model.

### 3. Dockerizing the Application
Using the **Dockerfile**, the Flask app is containerized to ensure consistency across environments. The Dockerfile installs all dependencies specified in \`requirements.txt\` and runs the application inside a container.

### 4. Deployment on GKE
The containerized application is deployed on **Google Kubernetes Engine (GKE)**. Kubernetes configuration files such as \`deployment.yaml\` and \`service.yaml\` (not included in this repository but necessary for deployment) are used to define the deployment specifications and expose the service.

### 5. API Usage
Once deployed, the API can be accessed via the exposed external IP address. Users can send POST requests with input features to get predictions from the model.

## How to Run the Project

### 1. Clone the Repository
\`\`\`bash
git clone https://github.com/<your-username>/<your-repository>.git
cd <your-repository>
\`\`\`

### 2. Build the Docker Image
\`\`\`bash
docker build -t insurance-predictor .
\`\`\`

### 3. Push Docker Image to Google Cloud Container Registry
\`\`\`bash
docker tag insurance-predictor gcr.io/<your-project-id>/insurance-predictor
docker push gcr.io/<your-project-id>/insurance-predictor
\`\`\`

### 4. Deploy on Google Kubernetes Engine (GKE)
- Ensure you have configured the \`deployment.yaml\` and \`service.yaml\` for Kubernetes deployment.
- Deploy the app on GKE:
\`\`\`bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
\`\`\`

### 5. Access the Prediction API
Use the external IP provided by GKE to make a POST request:
\`\`\`bash
curl -X POST http://<external-ip>/predict -H "Content-Type: application/json" -d '{"age": 45, "gender": "Male", "vehicle_type": "SUV", "annual_premium": 5000, "policy_sales_channel": "Direct"}'
\`\`\`

### Example Input
\`\`\`json
{
  "age": 45,
  "gender": "Male",
  "vehicle_type": "SUV",
  "annual_premium": 5000,
  "policy_sales_channel": "Direct"
}
\`\`\`

### Example Response
\`\`\`json
{
  "prediction": "Claim"
}
\`\`\`

## Future Improvements

- Add **CI/CD pipeline** using Google Cloud Build for continuous deployment.
- Explore more advanced feature engineering to improve model performance.
- Implement version control for models using **MLflow** or **DVC**.
- Deploy the app with **HTTPS** for secure connections.

## References

- [PyCaret Documentation](https://pycaret.org/)
- [Flask Documentation](https://flask.palletsprojects.com/en/2.0.x/)
- [Google Kubernetes Engine (GKE) Documentation](https://cloud.google.com/kubernetes-engine/docs)
- [Docker Documentation](https://docs.docker.com/)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
