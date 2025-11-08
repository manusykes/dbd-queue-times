from flask import Flask, Response
import requests
from bs4 import BeautifulSoup

app = Flask(__name__)

@app.route("/")
def get_queue_times():
    try:
        url = "https://www.deadbyqueue.com/region/eu-central-1"
        page = requests.get(url, timeout=10)
        soup = BeautifulSoup(page.text, "html.parser")

        killer = soup.select_one("div[data-role='killer'] span.queue-time")
        survivor = soup.select_one("div[data-role='survivor'] span.queue-time")

        killer_time = killer.text.strip() if killer else "N/A"
        surv_time = survivor.text.strip() if survivor else "N/A"

        result = f"Killer: {killer_time} | Survivor: {surv_time}"
        return Response(result, mimetype="text/plain")

    except Exception as e:
        return Response(f"Fehler: {e}", mimetype="text/plain")

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)
