from phi.agent import Agent
from phi.model.groq import Groq
from phi.tools.yfinance import YFinanceTools
from phi.tools.duckduckgo import DuckDuckGo
import openai

## Defining Keys for the API endpoints that are generated for the users, these can be moved into env files as secrets.
OPENAI_API_KEY=''
API_KEY=''
GROQ_API_KEY=''

## web search agent using Groq + llama3 model
## Define the agent with name, role, model, tools, instructions, show_tools_call, markdown
web_search_agent=Agent(
    name="Web Search Agent",
    role="Search the web for the information",
    model=Groq(id="llama3-groq-70b-8192-tool-use-preview"),
    tools=[DuckDuckGo()],
    instructions=["Alway include sources"],
    show_tools_calls=True,
    markdown=True,

)

## Financial agent using Groq and llama3 model
finance_agent=Agent(
    name="Finance AI Agent",
    model=Groq(id="llama3-groq-70b-8192-tool-use-preview"),
    tools=[
        YFinanceTools(stock_price=True, analyst_recommendations=True, stock_fundamentals=True,
                      company_news=True),
    ],
    instructions=["Use tables to display the data"],
    show_tool_calls=True,
    markdown=True,

)

## connecting agents using another agent. 
## Define team of agents, instructions, show_tool_calls and markdown
multi_ai_agent=Agent(
    team=[web_search_agent,finance_agent],
    instructions=["Always include sources","Use table to display the data"],
    show_tool_calls=True,
    markdown=True,
)

## calling multi agent with instructions. 
multi_ai_agent.print_response("Summarize analyst recommendation and share the latest news for NVDA",stream=True)
