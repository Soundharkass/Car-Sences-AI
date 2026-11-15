# Car Senses AI

Car Senses AI analyzes an uploaded road video, matches a detected vehicle against a small built-in car list, estimates its motion, and compares its published specs with similar cars.

## Run the main analyzer

From this folder, create and activate a virtual environment, install the dependencies, then start Streamlit:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
streamlit run app.py
```

The first run may download the selected YOLO and CLIP models. The app includes `yolov8n.pt`; the larger detector and CLIP choices need additional downloads.

## Use the vision-only analyzer

`car.py` samples frames and asks an OpenAI vision model for a likely make and model. Set `OPENAI_API_KEY` in the environment, or create `.streamlit/secrets.toml` from the example file and add your key there. Then run:

```powershell
streamlit run car.py
```

Keep the key private. Do not put it in Python source or commit `secrets.toml`.

## What the results mean

- Make/model matching is a best guess among the vehicles in the app's specs table. It may miss cars that are not listed.
- Speed and acceleration are estimates based on image movement and the selected scale. A moving camera, perspective, zoom, or a non-side-on view can make them inaccurate.
- Built-in vehicle specifications are approximate. Use a custom CSV with columns `brand,model,hp,accel_0_100,top_speed,weight` to supply another list.
- The acceleration chart is a simplified physics simulation, not a measured road test.
