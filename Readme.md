# Streamlit Cookie Tutorial 

## Corresponding Bilibili video

https://www.bilibili.com/video/BV1pr4y177rK/

## Example Code

app.py:

```python
import os
import streamlit as st

from extra_streamlit_components import CookieManager

# This should be on top of your script
import datetime
st.write("# Cookie Manager")

@st.cache(allow_output_mutation=True)
def get_manager():
    return CookieManager()

cookie_manager = get_manager()

st.subheader("All Cookies:")
cookies = cookie_manager.get_all()
st.write(cookies)

st.write(cookie_manager.get("name"))
st.write(cookie_manager.get("email"))
st.write(cookie_manager.get("phonenumber"))

c1, c2, c3 = st.columns(3)

with c1:
    st.subheader("Get Cookie:")
    cookie = st.text_input("Cookie", key="0")
    clicked = st.button("Get")
    if clicked:
        value = cookie_manager.get(cookie=cookie)
        st.write(value)
with c2:
    st.subheader("Set Cookie:")
    cookie = st.text_input("Cookie", key="1")
    val = st.text_input("Value")
    if st.button("Add"):
        cookie_manager.set(cookie, val, expires_at=datetime.datetime(year=2023, month=2, day=2))
with c3:
    st.subheader("Delete Cookie:")
    cookie = st.text_input("Cookie", key="2")
    if st.button("Delete"):
        cookie_manager.delete(cookie)
        
        
```

Run the application:
```shell
streamlit run app.py
```
