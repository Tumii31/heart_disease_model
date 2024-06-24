# heart_disease_model
import streamlit as st
import pandas as pd
import joblib

# Load the saved model
model = joblib.load('heart_disease_model.pkl')

# Create a Streamlit application
st.title('Heart Disease Prediction')
st.header('Enter Patient Details')

# Create a form for the patient details
age = st.number_input('Age')
sex = st.selectbox('Sex', ['Male', 'Female'])
cp = st.selectbox('Chest Pain Type', ['Typical Angina', 'Atypical Angina', 'Non-Anginal Pain', 'Asymptomatic'])
trestbps = st.number_input('Resting Blood Pressure')
thalach = st.number_input('Maximum Heart Rate')
exang = st.selectbox('Exercise Induced Angina', ['Yes', 'No'])
oldpeak = st.number_input('ST Depression Induced by Exercise')
slope = st.selectbox('Slope of the Peak Exercise ST Segment', ['Upsloping', 'Flat', 'Downsloping'])
ca = st.selectbox('Number of Major Vessels Colored by Fluoroscopy', list(range(0, 5)))
thal = st.selectbox('Status of the Heart', ['Normal', 'Fixed Defect', 'Reversible Defect', 'Unknown'])

# Create a button to submit the form
if st.button('Predict'):
    # Create a DataFrame from the form data
    data = pd.DataFrame({
        'age': [age],
        'sex': [sex],
        'cp': [cp],
        'trestbps': [trestbps],
        'thalach': [thalach],
        'exang': [exang],
        'oldpeak': [oldpeak],
        'slope': [slope],
        'ca': [ca],
        'thal': [thal]
    })

    # Make a prediction using the model
    prediction = model.predict(data)

    # Display the prediction
    st.header('Prediction')
    if prediction[0] == 1:
        st.write('The patient likely suffers from heart disease.')
    else:
        st.write('The patient does not likely suffer from heart disease.')
