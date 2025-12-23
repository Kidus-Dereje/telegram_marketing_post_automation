Telegram Social Media Posting Automation
📱 Overview
The Telegram Social Media Posting Automation is an intelligent workflow that extracts product information from user-uploaded images and creates professional social media posts. This n8n workflow uses computer vision, AI analysis, and automated content generation to transform product photos into detailed social media content with technical specifications and professionally sourced images.

✨ Key Features
Image-to-Text Extraction: Uses AWS Rekognition to extract text from product photos

Smart Text Processing: Deduplicates and filters extracted text for meaningful content

AI Product Analysis: Groq LLM identifies brand, product type, and specifications from extracted text

Professional Image Sourcing: Searches Bing Images for high-quality product photography

Automated Social Media Posting: Creates multi-image posts with detailed captions

Telegram Integration: Complete bot functionality for user interaction and content delivery

🏗️ Architecture
Workflow Components
Trigger: Telegram message with photo upload

Image Processing: AWS Rekognition for OCR and text extraction

AI Analysis: Groq LLM for product identification and specification extraction

Image Search: SerpAPI Bing search for professional product images

Content Assembly: Image downloading and caption formatting

Delivery: Multi-image Telegram post with technical specifications

Node Flow
text
Telegram Photo → OCR → Text Processing → AI Analysis → Image Search → Download → Telegram Post
🚀 Setup Instructions
Prerequisites
n8n Account: Self-hosted or cloud instance

Telegram Bot: Created via @BotFather

API Keys:

AWS Rekognition (for OCR)

Groq API (for LLM analysis)

SerpAPI (for Bing image search)

Telegram Bot Token

Step-by-Step Configuration
1. Telegram Bot Setup
Open Telegram and search for @BotFather

Create a new bot with /newbot

Save the bot token provided

Enable the bot to receive photos and messages

Start a conversation with your bot in Telegram

2. AWS Rekognition Setup
Create an AWS account (free tier available)

Navigate to IAM and create a new user with AmazonRekognitionFullAccess policy

Generate access keys (Access Key ID and Secret Access Key)

Configure these in the "Analyze image1" node

3. API Credentials Configuration
Groq API
Get API key from console.groq.com

Configure in "Groq Chat Model1" node

Model used: openai/gpt-oss-20b

SerpAPI (Bing Image Search)
Sign up at serpapi.com

Get your API key

Configure in "Bing_images search" node

Telegram Bot Token
Add your bot token to:

"Telegram Trigger" node (for receiving messages)

"Get a file" node

All "Send a photo message" nodes

"Send a text message" node

3. Workflow Import
Copy the provided JSON

In n8n: Workflows → Import from JSON

Update all credentials in the relevant nodes

4. Node Configuration Checklist
Telegram Trigger: Add bot token and configure webhook

AWS Rekognition: Add AWS credentials (Access Key ID and Secret Access Key)

Groq Chat Model1: Add Groq API key

SerpApi (Bing_images search): Add SerpAPI key

All Telegram nodes: Verify bot token is correctly configured

📱 User Workflow
How to Use the Bot
Start the Conversation:

Open Telegram and find your bot

Send /start to begin

Upload Product Photo:

Send a clear photo of a product with visible text

The photo should show labels, specifications, or branding

Wait for Processing:

Bot will analyze the image (30-60 seconds)

Multiple processing steps occur automatically

Receive Results:

Bot sends 3 professionally sourced product images

Detailed caption with brand, type, and specifications

All in a single, well-formatted post

Example Use Cases
E-commerce sellers: Create product listings from physical items

Retail employees: Generate social media content from store products

Product reviewers: Automate technical specification extraction

Social media managers: Create professional product posts quickly

🔧 Customization Options
Image Processing
Modify the "Extract Unique Texts" node to:

Change text filtering logic

Adjust minimum text length

Modify deduplication rules

Change substring filtering behavior

Product Analysis
Adjust the AI prompt in "Basic LLM Chain" to:

Change specification extraction criteria

Modify brand detection logic

Adjust number of specifications extracted

Change response formatting

Image Search
Modify "Parse Response" node to:

Change search query construction

Adjust image search terms

Modify background preferences

Change result prioritization

Social Media Formatting
Customize "Format Caption" node to:

Change caption structure

Modify Markdown/formatting

Adjust technical specification presentation

Change branding emphasis

🛠️ Technical Details
Nodes Used
n8n Core: Telegram Trigger, Code, Merge, HTTP Request

AWS: Rekognition (OCR)

LangChain: ChainLlm, LmChatGroq

Community: SerpApi (Bing search)

Key Code Snippets

Image Text Extraction (Extract Unique Texts node)
javascript
// Processes AWS Rekognition output
// Deduplicates, filters, and sorts detected text
// Removes substrings to keep only meaningful phrases

Product Analysis (Parse Response node)
javascript
// Parses LLM output for brand, type, and specs
// Constructs optimized search query for product images
// Includes model numbers when available

Image Processing Pipeline (Download Image nodes)
javascript
// Downloads top 3 images from Bing search
// Uses separate HTTP requests for parallel downloading
// Handles errors gracefully with continueRegularOutput

🔒 Security & Best Practices
API Security
Use Environment Variables for all API keys

Rotate AWS credentials regularly

Monitor API usage to avoid rate limits

Use webhook secrets for Telegram bot security

Data Privacy
User photos are processed through AWS Rekognition

Extracted text is sent to Groq for analysis

No user data is stored permanently in the workflow

Consider GDPR compliance for EU users

Error Handling
The workflow includes:

Graceful error handling with continueRegularOutput

Input validation for all processing steps

Fallback behavior when images aren't found

User-friendly error messages in Telegram

📊 Monitoring & Maintenance
Success Indicators
Successful photo upload and processing

Relevant product images found and sent

Accurate brand and specification extraction

User satisfaction with generated posts

Common Issues & Solutions
Issue	Solution
No text detected	Improve photo quality, ensure text is visible
Wrong brand identified	Adjust LLM prompt for better brand detection
No images found	Modify search query construction
Telegram sending fails	Check bot token, verify chat permissions
AWS Rekognition errors	Check IAM permissions, verify region settings
Performance Optimization
Image Size: Telegram compresses images - request highest quality

Parallel Processing: Images download simultaneously

Caching: Consider caching frequently analyzed products

Batching: Process multiple images in sequence if needed

🚨 Limitations & Considerations
Current Limitations
Image Quality Dependency: Requires clear, readable text

Brand Recognition: May not identify obscure brands

Language Support: Primarily English text recognition

Image Availability: Depends on Bing search results

Ethical Considerations
Respect copyright for sourced images

Disclose automated content generation

Ensure product claims are accurate

Respect user privacy and data

Cost Management
AWS Rekognition: Pay-per-use pricing

Groq API: Token-based pricing

SerpAPI: Monthly subscription with usage limits

Monitor usage to avoid unexpected costs

🤝 Support & Troubleshooting
Getting Help
n8n Community: community.n8n.io

Telegram Bot API: core.telegram.org/bots

AWS Rekognition Docs: AWS documentation

Groq Support: Developer documentation

Debugging Tips
Test Each Node: Use n8n's test functionality

Check Webhooks: Ensure Telegram webhook is properly configured

API Limits: Monitor usage across all services

User Permissions: Verify all API credentials have correct permissions

📄 License & Compliance
Ensure compliance with:

Telegram Bot Terms of Service

AWS Service Terms

Groq API Usage Policies

SerpAPI Terms of Service

Copyright laws for image usage

Attribution Requirements
Disclose automated content generation if required

Credit image sources when applicable

Comply with platform-specific automation rules

*Built with n8n - The extendable workflow automation tool.*
Perfect for e-commerce, retail, and social media management.
Last Updated: 23/12/2025