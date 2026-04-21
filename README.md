# app.py - استخدام Flask + Streamlit
import streamlit as st
import pandas as pd
import plotly.express as px

st.set_page_config(page_title="Data Analytics", layout="wide")

st.title("📊 Data Analytics Dashboard")
st.markdown("---")

# رفع البيانات
uploaded_file = st.file_uploader("Choose CSV file", type="csv")

if uploaded_file:
    df = pd.read_csv(uploaded_file)
    
    col1, col2 = st.columns(2)
    
    with col1:
        st.subheader("📋 Data Preview")
        st.dataframe(df.head())
    
    with col2:
        st.subheader("📊 Statistics")
        st.write(df.describe())
    
    # Visualizations
    st.subheader("📈 Charts")
    chart = px.bar(df, x=df.columns[0], y=df.columns[1])
    st.plotly_chart(chart, use_container_width=True)
