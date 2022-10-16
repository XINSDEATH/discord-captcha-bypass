# discord-captcha-bypass


**use bypass.py to bypass any captcha, for example**:

```
import requests, fade, time, httx

headers = None
for i in range(15):
            try:
                createTask = httpx.post(            "https://api.capmonster.cloud/createTask", json={
                        "clientKey": settings["capmonsterKey"],     "task": {
                            "type": "HCaptchaTaskProxyless",         "websiteURL": "https://discord.com/channels/@me",         "websiteKey":
                            "4c672d35-0701-42b2-88c3-78380b0db560"
                        }
                    }).json()["taskId"]

                print(fade.pinkred(f"Captcha Task: {createTask}"))

                getResults = {}
                getResults["status"] = "processing"
                while getResults["status"] == "processing":
                    getResults = httpx.post(                "https://api.capmonster.cloud/getTaskResult",     json={
                            "clientKey": settings["capmonsterKey"],         "taskId": createTask
                        }).json()

                    time.sleep(1)

                solution = getResults["solution"]["gRecaptchaResponse"]

                print(fade.pinkred(f"Captcha Solved"))

                join_server = requests.post(            f"https://discord.com/api/v9/invites/invite", headers=headers, json={"captcha_key": solution})
                print(join_server)
                break
            except:
                pass
```
