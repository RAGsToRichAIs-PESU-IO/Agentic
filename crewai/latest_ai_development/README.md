# Assignment 2: Building an Agentic Application with Web Search Capabilities

## Overview
In this assignment, you will create a multi-agent system using CrewAI that leverages web search capabilities. You'll implement at least two agents that work together to process and analyze web search results.

## Learning Objectives
- Implement a multi-agent system using CrewAI
- Integrate web search capabilities using SerperDevTool
- Design agent interactions for data processing and analysis
- Practice working with YAML configurations for agent definitions

## Requirements

### Technical Prerequisites
- Python 3.111-3.12
- CrewAI and CrewAI-tools packages
- Serper.dev API key

### Core Requirements
1. Implement at least two agents:
   - Agent 1: Must utilize SerperDevTool for web searching
   - Agent 2: Must process/analyze the data from Agent 1
2. Configure agents using YAML
3. Implement proper error handling
4. Include documentation

## Setup Instructions

### 1. Environment Setup
```bash
# Install required packages
pip install crewai

# Create new CrewAI project
crewai create crew your_project_name
```

### 2. SerperDevTool Configuration
```python
from crewai_tools import SerperDevTool

# Initialize the search tool
search_tool = SerperDevTool()
```

### 3. YAML Configuration Examples

#### agents.yaml
```yaml
search_agent:
  name: "Web Search Agent"
  role: "Internet Researcher"
  goal: "Search and collect relevant information from the web"
  backstory: "Expert at finding and collecting relevant information from internet sources"
  tools:
    - SerperDevTool
  allow_delegation: true

analysis_agent:
  name: "Data Analysis Agent"
  role: "Data Analyst"
  goal: "Process and analyze web search results to extract meaningful insights"
  backstory: "Specialized in analyzing and synthesizing information from various sources"
  tools: []
  allow_delegation: false
```

#### tasks.yaml
```yaml
tasks:
  - name: web_search
    description: "Search the web for specified query"
    agent: search_agent
    expected_output: "Raw search results"
    
  - name: analyze_results
    description: "Analyze and process search results"
    agent: analysis_agent
    expected_output: "Processed insights and analysis"
    depends_on: web_search
```

## Sample Implementation Structure
```python
from crewai import Crew, Agent, Task
from crewai_tools import SerperDevTool

# Initialize tools
search_tool = SerperDevTool()

# Create agents
search_agent = Agent(
    name="Web Search Agent",
    role="Internet Researcher",
    goal="Search and collect relevant information from the web",
    backstory="Expert at finding and collecting relevant information from internet sources",
    tools=[search_tool]
)

analysis_agent = Agent(
    name="Data Analysis Agent",
    role="Data Analyst",
    goal="Process and analyze web search results to extract meaningful insights",
    backstory="Specialized in analyzing and synthesizing information from various sources"
)

# Create tasks
search_task = Task(
    description="Search the web for [YOUR_QUERY]",
    agent=search_agent
)

analysis_task = Task(
    description="Analyze the search results and provide insights",
    agent=analysis_agent
)

# Create and run crew
crew = Crew(
    agents=[search_agent, analysis_agent],
    tasks=[search_task, analysis_task]
)

result = crew.kickoff()
```

## Evaluation Criteria
- Functionality (40%)
  - Proper implementation of web search
  - Effective agent interaction
  - Accurate data processing
- Code Quality (30%)
  - Clean, well-organized code
  - Proper error handling
  - Effective use of YAML configuration
- Documentation (20%)
  - Clear setup instructions
  - Well-documented code
  - Usage examples
- Creativity (10%)
  - Innovative use of agents
  - Original application concept

## Submission Guidelines
1. Submit your code via GitHub repository
2. Include:
   - All source code
   - YAML configuration files
   - Requirements.txt or environment.yml
   - README with setup and usage instructions
   - Sample output demonstrating functionality



## Resources
- [CrewAI Documentation](https://docs.crewai.com/)
