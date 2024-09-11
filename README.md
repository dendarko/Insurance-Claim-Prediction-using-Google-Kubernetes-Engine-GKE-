
# Insurance Claim Prediction Pipeline Deployment on Google Kubernetes Engine (GKE)

## Project Overview

This project demonstrates the end-to-end process of deploying a machine learning pipeline on **Google Kubernetes Engine (GKE)** for predicting the likelihood of insurance claims. The pipeline includes model training, API development, containerization, and deployment, showcasing a robust, scalable cloud-based solution. The key goal is to provide real-time predictions based on user inputs related to customer demographics, vehicle details, and insurance-related features.

The pipeline leverages **PyCaret** for model development, **Flask** for API creation, **Docker** for containerization, and **Google Cloud Platform (GCP)** for infrastructure and deployment management.

---

## Key Technologies

- **Google Kubernetes Engine (GKE)**: Orchestrates the deployment and management of containerized applications.
- **Flask**: A Python-based web framework used to build a REST API for serving the model.
- **Docker**: Provides containerization to ensure consistent environments across deployments.
- **PyCaret**: A low-code machine learning library used for training the predictive model.
- **Google Cloud Platform (GCP)**: Provides cloud infrastructure for storage, container management, and deployment.
- **Python**: Core programming language for model development, API logic, and script management.

---

## Project Structure

Here's a breakdown of the main components in this repository:

- **`Dockerfile`**: Instructions for building the Docker image containing the Flask API and ML model.
- **`app.py`**: The Flask web application that exposes the model for real-time predictions.
- **`config.py`**: Configuration settings for the Flask application.
- **`deployment_28042020.pkl`**: The pre-trained PyCaret model serialized for deployment.
- **`requirements.txt`**: Lists all Python dependencies necessary for running the Flask API.
- **`templates/home.html`**: The frontend HTML interface for the web app.
- **`static/style.css`**: CSS file for styling the HTML interface.
- **`Insurance - Model Training Notebook.ipynb`**: Jupyter notebook containing the model development and training code.
- **`.gcloudignore`**: Specifies files and directories to be ignored during GCP deployment.

---

## Workflow Overview

### 1. **Model Development and Training**
   The machine learning pipeline is developed using **PyCaret**, a low-code library. The model is trained in the Jupyter notebook `Insurance - Model Training Notebook.ipynb`, where data preprocessing, feature engineering, and model training take place. The model is saved as `deployment_28042020.pkl` for deployment.

### 2. **Flask API Development**
   The Flask API (`app.py`) exposes the trained machine learning model for predictions. It has an endpoint `/predict` that accepts input data in JSON format and returns a prediction.

   Example:
   ```json
   {
      "age": 45,
      "gender": "Male",
      "vehicle_type": "SUV",
      "annual_premium": 5000,
      "policy_sales_channel": "Direct"
   }
   ```

### 3. **Containerizing the Application**
   Using **Docker**, the application is containerized to ensure portability across environments. The `Dockerfile` contains instructions to install dependencies, configure the environment, and run the Flask application inside a container. This guarantees that the API works seamlessly across different machines and cloud platforms.

### 4. **Deployment on Google Kubernetes Engine (GKE)**
   The containerized application is deployed on **Google Kubernetes Engine**. Kubernetes manages the scaling, health checks, and distribution of containerized services. Using `deployment.yaml` and `service.yaml` files (not included in this repo), Kubernetes handles the deployment specifications, including replicas, load balancing, and exposing the app to the public via an external IP address.

### 5. **API Usage**
   Once the API is deployed on GKE, it can be accessed via the external IP. You can send a POST request with customer data to the `/predict` endpoint for real-time insurance claim predictions.

   Example POST request:
   ```bash
   curl -X POST http://<EXTERNAL-IP>/predict -H "Content-Type: application/json" -d '{"age": 45, "gender": "Male", "vehicle_type": "SUV", "annual_premium": 5000, "policy_sales_channel": "Direct"}'
   ```

   Example Response:
   ```json
   {
      "prediction": "Claim"
   }
   ```

---

## How to Run the Project

### 1. **Clone the Repository**
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   cd <your-repo>
   ```

### 2. **Build the Docker Image**
   ```bash
   docker build -t insurance-predictor .
   ```

### 3. **Push Docker Image to Google Cloud Container Registry**
   ```bash
   docker tag insurance-predictor gcr.io/<your-project-id>/insurance-predictor
   docker push gcr.io/<your-project-id>/insurance-predictor
   ```

### 4. **Deploy on Google Kubernetes Engine (GKE)**
   Ensure that you have configured the necessary `deployment.yaml` and `service.yaml` files for Kubernetes deployment, then:

   ```bash
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```

### 5. **Access the Prediction API**
   Once deployed, the API can be accessed via the external IP address provided by GKE. Use a tool like `curl` or Postman to send POST requests with the required features for predictions.

---

## Future Improvements

Here are some future enhancements that can improve the project:

1. **CI/CD Pipeline**: Implement a continuous integration/continuous deployment (CI/CD) pipeline using **Google Cloud Build** to automate the deployment process.
2. **Model Version Control**: Use tools like **MLflow** or **DVC** to implement version control for the machine learning models.
3. **HTTPS Deployment**: Secure the API by deploying it with **HTTPS** for encrypted communication.
4. **Advanced Feature Engineering**: Explore more advanced feature engineering techniques to further improve model performance.

---

## References

- [PyCaret Documentation](https://pycaret.org)
- [Flask Documentation](https://flask.palletsprojects.com/en/2.0.x/)
- [Google Kubernetes Engine (GKE) Documentation](https://cloud.google.com/kubernetes-engine/docs)
- [Docker Documentation](https://docs.docker.com/)

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
