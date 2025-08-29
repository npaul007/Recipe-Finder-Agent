# Agent Prompts

This directory contains the system prompts used by each agent in the Recipe Finder Agent workflow.

## Files

### `recipe_finder_agent_prompt.txt`

System prompt for the first agent in the sequence. This agent:

- Takes user criteria (favorite foods, allergies, dietary goals)
- Uses the Spoonacular API tool to search for recipes
- Passes results to the Recipe Pruner Agent

### `recipe_pruner_agent_prompt.txt`

System prompt for the second agent in the sequence. This agent:

- Receives JSON payload from Recipe Finder Agent
- Analyzes and filters recipes based on user criteria
- Returns 5 best-matching recipes in structured JSON format

## Usage

These prompts are configured in the Flowise agent nodes. To update:

1. Edit the `.txt` files in this directory
2. Copy the updated prompt text
3. Paste into the corresponding agent's "System Prompt" field in Flowise
4. Save the chatflow configuration

## Prompt Engineering Tips

- Keep prompts clear and specific about expected inputs/outputs
- Include examples where helpful
- Specify exact JSON structure requirements
- Test changes with various user queries to ensure consistent behavior
