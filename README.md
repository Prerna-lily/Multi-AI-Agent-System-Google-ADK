# Multi-AI-Agent-System-Google-ADK

## Overview
This project is a modular multi-agent system that takes a user goal, creates a plan, and routes data between agents, each enriching the output of the previous, until the goal is achieved. Agents depend on each other's outputs and iterate if the goal is not met.

### Example Goal
```
Find the next SpaceX launch, check weather at that location, then summarize if it may be delayed.
```

## Agent Flow
1. **Planner Agent**: Parses the user goal and creates a plan (sequence of agent actions).
2. **SpaceX Agent**: Fetches the next SpaceX launch details.
3. **Weather Agent**: Gets weather at the launch location using OpenWeatherMap API.
4. **Summary Agent**: Summarizes if the launch may be delayed based on weather.

## Setup
1. **Clone or unzip the repo**
2. **Install dependencies**:
   ```
   pip install -r requirements.txt
   ```
3. **Set up API keys**:
   - You can hardcode your OpenWeatherMap API key in `agents/weather_agent.py` as shown in the code, or use a `.env` file:
     ```
     OPENWEATHER_API_KEY=your_openweathermap_api_key
     ```
   - Get your API key from [OpenWeatherMap](https://openweathermap.org/api)

## Usage
Run the main script:
```
python main.py
```
Enter your goal when prompted (e.g., the example above).

## Evals
Run the evaluation script to test the agent chain and see the agent trajectory:
```
python evals/test_cases.py
```

### Example Eval Output
```
Agent Trajectory:
Agent: spacex_agent, Action: get_next_launch, Output: {'name': 'USSF-44', 'date_utc': '2022-11-01T13:41:00.000Z', 'location': 'KSC LC 39A', 'latitude': 28.6080585, 'longitude': -80.6039558, 'weather': {...}}
Agent: weather_agent, Action: get_weather_at_location, Output: {'name': 'USSF-44', 'date_utc': '2022-11-01T13:41:00.000Z', 'location': 'KSC LC 39A', 'latitude': 28.6080585, 'longitude': -80.6039558, 'weather': {...}}
Agent: summary_agent, Action: summarize_delay_risk, Output: Launch: USSF-44 at KSC LC 39A on 2022-11-01T13:41:00.000Z
Weather: Clouds, Wind Speed: 4.73 m/s
Weather conditions look favorable for launch....

Final Output:
 Launch: USSF-44 at KSC LC 39A on 2022-11-01T13:41:00.000Z
Weather: Clouds, Wind Speed: 4.73 m/s
Weather conditions look favorable for launch.
```

## APIs Used
- [SpaceX API](https://github.com/r-spacex/SpaceX-API)
- [OpenWeatherMap API](https://openweathermap.org/api)

## Extending
- Add more agents for other APIs (e.g., CoinGecko, NewsAPI)
- Enhance planner logic for more complex goals

## Project Structure
```
multi_agent_system/
│
├── agents/
│   ├── planner.py
│   ├── spacex_agent.py
│   ├── weather_agent.py
│   └── summary_agent.py
│
├── main.py
├── evals/
│   └── test_cases.py
├── .env 
├── requirements.txt
└── README.md
```
