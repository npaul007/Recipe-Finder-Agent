# Recipe Finder Agent 🍳🤖

A sophisticated AI-powered recipe discovery application built with Flowise that helps users find personalized meal recipes based on their preferences, dietary restrictions, and health goals. This project demonstrates advanced AI agent orchestration using sequential agents and external API integration.

## 🌟 Features

- **Intelligent Recipe Discovery**: Uses the Spoonacular API to find recipes based on preferred ingredients
- **Multi-Agent Architecture**: Sequential agent workflow with specialized roles:
  - **Recipe Finder Agent**: Searches for recipes using specified ingredients
  - **Recipe Pruner Agent**: Filters and formats recipes based on dietary criteria
- **Personalized Filtering**: Considers user's favorite foods, allergies, and dietary goals
- **Structured JSON Output**: Returns clean, formatted recipe data with ingredients, directions, and images
- **AI-Powered Analysis**: Leverages OpenAI's GPT models for intelligent recipe curation

## 🏗️ Architecture

![Agent Flow Architecture](images/agent-flow-diagram.png)
_Sequential agent workflow showing the complete recipe discovery process_

The application uses a sequential agent pattern in Flowise:

1. **Start Node** → **Recipe Finder Agent** → **Recipe Pruner Agent** → **End Node**

### Agent Workflow:

1. **Recipe Finder Agent**: Takes user criteria and searches Spoonacular API for matching recipes
2. **Recipe Pruner Agent**: Analyzes the results and returns the 5 best recipes in a structured format

## 📋 Prerequisites

### Required Software

1. **Node.js** (v18 or higher)

   ```bash
   # Check your Node.js version
   node --version
   ```

2. **Flowise** - Install globally
   ```bash
   npm install -g flowise
   ```
   Or using Docker:
   ```bash
   docker pull flowiseai/flowise
   ```

### Required API Keys

#### 1. Spoonacular API Key

- Visit [Spoonacular API](https://spoonacular.com/food-api)
- Sign up for a free account
- Navigate to your profile and copy your API key
- **Important**: Replace the API key in the custom tool configuration

#### 2. OpenAI API Key (or Alternative LLM)

- Get an API key from [OpenAI](https://platform.openai.com/api-keys)
- Alternative LLM options:
  - **Anthropic Claude**: [Get API key](https://console.anthropic.com/)
  - **Google Gemini**: [Get API key](https://ai.google.dev/)
  - **Local LLMs**: Ollama, LM Studio, or similar
  - **Azure OpenAI**: Enterprise option

## 🚀 Installation & Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/Recipe-Finder-Agent.git
cd Recipe-Finder-Agent
```

### Step 2: Start Flowise

```bash
# Using npm installation
npx flowise start

# Or using Docker
docker run -d --name flowise -p 3000:3000 flowiseai/flowise
```

Flowise will be available at `http://localhost:3000`

![Flowise Dashboard](images/flowise-dashboard.png)
_Flowise dashboard interface_

### Step 3: Import Custom Tool

Before configuring API keys, you need to import the Spoonacular tool:

1. In Flowise dashboard, navigate to **Tools** section
2. Click **"Import Tool"** or **"Add Tool"**
3. Upload the `tools/spoonacular_recipe_finder-CustomTool.json` file
4. Save the imported tool

![Import Tool](images/import-tool.png)
_Importing the Spoonacular custom tool_

### Step 4: Configure API Keys

#### Configure Spoonacular API Key:

1. After importing the tool, edit the **spoonacular_recipe_finder** tool
2. In the **Function** section, replace the existing API key:
   ```javascript
   const apiKey = "YOUR_SPOONACULAR_API_KEY_HERE";
   ```
3. Save the tool configuration

![Configure Spoonacular API](images/configure-spoonacular-api.png)
_Configuring the Spoonacular API key in the custom tool_

#### Configure OpenAI Credentials in Flowise:

1. Navigate to Flowise dashboard (`http://localhost:3000`)
2. Go to **Settings** → **Credentials**
3. Add new credential with type **OpenAI API**
4. Enter your OpenAI API key

![OpenAI Credentials](images/openai-credentials.png)
_Adding OpenAI credentials in Flowise_

### Step 5: Import the Agent Flow

1. In Flowise dashboard, click **"Import Chatflow"**
2. Upload the `agent/Recipe Finder Agent Agents.json` file
3. The chatflow will be imported with all agent configurations

![Import Chatflow](images/import-chatflow.png)
_Importing the Recipe Finder Agent chatflow_

### Step 6: Link the Custom Tool

1. Open the imported chatflow
2. Ensure the **Custom Tool** node is linked to the **Recipe Finder Agent**
3. In the Custom Tool node, select the imported **spoonacular_recipe_finder** tool
4. Verify all connections between nodes are intact

![Link Custom Tool](images/link-custom-tool.png)
_Linking the Spoonacular tool to the Recipe Finder Agent_

![Complete Flow](images/complete-agent-flow.png)
_Complete agent flow with all nodes connected_

## 🎯 Usage

![Usage Example](images/usage-example.png)
_Example conversation with the Recipe Finder Agent_

### Example Query Format:

```
I love chicken, broccoli, and rice. I'm allergic to nuts and dairy.
I want to build muscle and eat high-protein meals.
```

### Expected Response:

The agent will return a JSON object with 5 curated recipes:

```json
{
  "recipes": [
    {
      "name": "High-Protein Chicken and Broccoli Bowl",
      "description": "A nutritious muscle-building meal with lean protein and vegetables",
      "directions": [
        "Season chicken breast with salt and pepper",
        "Heat oil in pan and cook chicken until golden",
        "Steam broccoli until tender",
        "Serve over cooked rice"
      ],
      "ingredients": [
        "1 lb chicken breast",
        "2 cups broccoli florets",
        "1 cup brown rice",
        "2 tbsp olive oil"
      ],
      "imageUrls": "https://spoonacular.com/recipeImages/..."
    }
  ]
}
```

## 🔧 Configuration

![Agent Configuration](images/agent-configuration.png)
_Configuring agent system prompts and parameters_

### Customizing the Agents

#### Recipe Finder Agent System Prompt:

Located in the agent configuration, you can modify the search criteria and behavior.

#### Recipe Pruner Agent System Prompt:

Customize the filtering logic and output format requirements.

### Tool Parameters

The Spoonacular tool accepts:

- **ingredients**: Comma-separated list of ingredients (e.g., "chicken, broccoli, garlic")

## 🐛 Troubleshooting

![Debug Interface](images/debug-interface.png)
_Flowise debug interface showing execution logs_

### Common Issues:

1. **API Key Errors**

   - Verify Spoonacular API key is valid and has available requests
   - Check OpenAI API key has sufficient credits

2. **Tool Not Found**

   - Ensure custom tool is properly imported and linked to the agent
   - Verify tool ID matches in the agent configuration

3. **Flow Execution Errors**
   - Check all nodes are properly connected
   - Verify agent memory is configured if using stateful conversations

### Debug Mode:

Enable debug logging in Flowise settings to see detailed execution logs.

## 📊 API Limits

- **Spoonacular Free Tier**: 150 requests/day
- **OpenAI Rates**: Vary by model and tier

Monitor your usage to avoid hitting rate limits.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Flowise](https://github.com/FlowiseAI/Flowise) - Low-code LLM apps builder
- [Spoonacular API](https://spoonacular.com/food-api) - Recipe and nutrition data
- [OpenAI](https://openai.com/) - GPT models for intelligent processing

---

**Made with ❤️ to showcase AI proficiency and agent orchestration capabilities**
