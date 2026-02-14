# smart-home-control-app-IoT-
built an smart home control of appliances through IoT using streamlit and python


import streamlit as st
import random
import time

# ------------------------------
# Page Configuration
# ------------------------------
st.set_page_config(
    page_title="Smart Home Control Panel",
    page_icon="🏠",
    layout="wide"
)

# ------------------------------
# Initialize Session State
# ------------------------------
if "light" not in st.session_state:
    st.session_state.light = False

if "fan_speed" not in st.session_state:
    st.session_state.fan_speed = 0

if "door_locked" not in st.session_state:
    st.session_state.door_locked = True

if "temperature" not in st.session_state:
    st.session_state.temperature = 25

# ------------------------------
# Title
# ------------------------------
st.title("🏠 Smart Home Control Panel")
st.markdown("### Simulated IoT Device Control System")

st.divider()

# ------------------------------
# Layout Columns
# ------------------------------
col1, col2 = st.columns(2)

# ------------------------------
# Light Control
# ------------------------------
with col1:
    st.subheader("💡 Light Control")

    if st.button("Toggle Light"):
        st.session_state.light = not st.session_state.light

    if st.session_state.light:
        st.success("Light is ON")
    else:
        st.error("Light is OFF")

# ------------------------------
# Fan Control
# ------------------------------
with col2:
    st.subheader("🌪 Fan Control")

    st.session_state.fan_speed = st.slider(
        "Set Fan Speed",
        min_value=0,
        max_value=5,
        value=st.session_state.fan_speed
    )

    st.info(f"Current Fan Speed: {st.session_state.fan_speed}")

st.divider()

# ------------------------------
# Door Lock Control
# ------------------------------
st.subheader("🚪 Door Lock System")

if st.button("Lock / Unlock Door"):
    st.session_state.door_locked = not st.session_state.door_locked

if st.session_state.door_locked:
    st.success("Door is LOCKED 🔒")
else:
    st.warning("Door is UNLOCKED 🔓")

st.divider()

# ------------------------------
# Temperature Monitoring (Simulated)
# ------------------------------
st.subheader("🌡 Temperature Monitoring")

if st.button("Refresh Temperature"):
    st.session_state.temperature = random.randint(20, 35)

st.metric(
    label="Current Room Temperature",
    value=f"{st.session_state.temperature} °C"
)

st.divider()

# ------------------------------
# Energy Usage Estimation
# ------------------------------
st.subheader("⚡ Energy Usage Estimation")

energy_usage = (
    (10 if st.session_state.light else 0) +
    (st.session_state.fan_speed * 15)
)

st.metric(
    label="Estimated Energy Consumption",
    value=f"{energy_usage} Watts"
)

st.divider()

# ------------------------------
# Footer
# ------------------------------
st.markdown(
    """
    ---
    Developed using *Python & Streamlit*
    """
)
