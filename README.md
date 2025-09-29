# Rasa Broadcast Bot

## Purpose
The **Rasa Broadcast Bot** is a conversational AI system designed for healthcare professionals to manage and distribute broadcast messages. This Rasa-based chatbot enables doctors to create, configure, and retrieve broadcast communications for patient outreach, announcements, and healthcare updates through an intuitive conversational interface.

## Operational Flow

The bot operates through the following 7-step process:

1. **User Greeting & Intent Recognition**: The bot greets users and identifies their intent (add broadcast, get broadcast, or general conversation)

2. **Form Activation**: Based on the detected intent, the bot activates the appropriate form:
   - `broadcast_form` for creating new broadcasts
   - `get_broadcast_form` for retrieving existing broadcasts

3. **Data Collection**: The bot systematically collects required information through slot filling:
   - For broadcast creation: name, type, description, media, recipients
   - For broadcast retrieval: broadcast title

4. **Input Validation**: Custom validation logic ensures data quality:
   - Name validation (alphabetic characters and multi-word check)
   - Type validation (announcement, news, tv)
   - Recipients validation (numeric format)

5. **Backend Integration**: The bot communicates with external APIs through the BackendManager:
   - Token generation for authentication
   - API calls to add or retrieve broadcast data

6. **Response Generation**: The bot provides confirmation messages and results to the user

7. **Session Management**: Automatic slot reset and session cleanup after form completion

## Project Structure

```
rasa_brodcast_bot/
├── actions/
│   ├── actions.py          # Custom actions and form validation logic
│   ├── endpoints.py        # Backend API integration and token management
│   └── __init__.py
├── data/
│   ├── nlu.yml            # Natural language understanding training data
│   ├── rules.yml          # Conversation rules and form handling
│   └── stories.yml        # Training stories and conversation flows
├── config.yml             # Rasa pipeline and policy configuration
├── domain.yml             # Bot domain with intents, slots, and responses
├── credentials.yml        # Channel configuration templates
├── endpoints.yml          # Action server and other endpoint configurations
└── tests/
    └── test_stories.yml   # Test scenarios for validation
```

## Language
**Python** - The entire project is implemented in Python, leveraging the Rasa framework for conversational AI development.

## Tools Used

### Core Framework
- **Rasa Framework**: Open-source conversational AI platform
- **Rasa SDK**: Software Development Kit for custom actions

### NLU Pipeline Components
- **WhitespaceTokenizer**: Text tokenization
- **RegexFeaturizer**: Regular expression-based feature extraction
- **LexicalSyntacticFeaturizer**: Linguistic feature extraction
- **CountVectorsFeaturizer**: N-gram and character-level features
- **DIETClassifier**: Dual Intent and Entity Transformer for intent classification
- **EntitySynonymMapper**: Entity synonym mapping
- **ResponseSelector**: Response selection for retrieval-based responses
- **FallbackClassifier**: Fallback intent handling

### Core Policies
- **MemoizationPolicy**: Exact story matching
- **RulePolicy**: Rule-based conversation handling
- **UnexpecTEDIntentPolicy**: Unexpected intent handling
- **TEDPolicy**: Transformer Embedding Dialogue policy

### Custom Components
- **FormValidationAction**: Custom form validation logic
- **BackendManager**: API integration and token management
- **Custom Actions**: Slot reset, restart, and form submission actions

### External Integrations
- **REST API**: Backend communication for broadcast management
- **Token-based Authentication**: Secure API access
- **Healthcare API Integration**: Specialized medical broadcast system

The bot is designed specifically for healthcare environments, providing a user-friendly interface for medical professionals to manage patient communications and broadcast important health information efficiently.
