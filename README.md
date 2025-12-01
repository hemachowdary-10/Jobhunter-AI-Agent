

this agent is based on  upcoming open-source framework help devs instantly build fast & reliable AI agents that can control browsers autonomously in 3 lines of code. 

# jobhunter - apply to relevant jobs on internet autonomously

jobhunter is an ai agent that searches and applies for jobs on your behalf by controlling your browser. put in your resume and preferences and it does the work in background.


### jobhunter and jobhunter_fsm

you might notice two separate implementations of jobhunter in the repo. `jobhunter` folder contains a simpler approach to implementing multi-agent conversation required between a planner and a browser agent.

the `jobhunterer_fsm` folder contains another approach based on [finite state machines]. there are slight nuances and both result in similar level or performace. 


### setup

1. we recommend installing poetry before proceeding with the next steps. you can install poetry using these [instructions](https://python-poetry.org/docs/#installation)

2. install dependencies

```bash
poetry install
```

3. start chrome in dev mode - in a seaparate terminal, use the command to start a chrome instance and do necesssary logins to job websites like linkedin/ wellfound, etc.

for mac, use command -

```bash
sudo /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222
```

for linux -

```bash
google-chrome --remote-debugging-port=9222
```

for windows -

```bash
"C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222
```

4. set up env - add openai and [langsmith](https://smith.langchain.com) keys to .env file. you can refer .env.example. currently adding langsmith is required but if you do not want to use it for tracing - then you can comment the line `litellm.success_callback = ["langsmith"]` in the `./jobhunter_fsm/core/agent/base.py` file.

5. update your preferences in the `user_preferences.txt` file in the folder of agent that you are running (jobhunter/ jobhunter_fsm). provide the local file path to your resume in this file itself for the agent to be able to upload it.

6. run the agent - jobhunter_fsm or jobhuter

```bash
python -u -m jobhunter_fsm
```

or

```bash
python -u -m jobhunter
```

6. enter your task. sample task -

```bash
apply for a backend engineer role based on linkedin
```

### Run evals

1. For Jobhunter

```bash
 python -m test.tests_processor --orchestrator_type vanilla
```

2. For Jobhunter FSM

```bash
 python -m test.tests_processor --orchestrator_type fsm
```

