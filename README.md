# Telegram Social Media Posting Automation

## 📱 Overview

The Telegram Social Media Posting Automation is an intelligent workflow that extracts product information from user-uploaded images and creates professional social media posts. This n8n workflow uses computer vision, AI analysis, and automated content generation to transform product photos into detailed social media content with technical specifications and professionally sourced images.

## ✨ Key Features

- **Image-to-Text Extraction**: Uses AWS Rekognition to extract text from product photos
- **Smart Text Processing**: Deduplicates and filters extracted text for meaningful content
- **AI Product Analysis**: Groq LLM identifies brand, product type, and specifications from extracted text
- **Professional Image Sourcing**: Searches Bing Images for high-quality product photography
- **Automated Social Media Posting**: Creates multi-image posts with detailed captions
- **Telegram Integration**: Complete bot functionality for user interaction and content delivery

## 🏗️ Architecture

### Workflow Components

1. **Trigger**: Telegram message with photo upload
2. **Image Processing**: AWS Rekognition for OCR and text extraction
3. **AI Analysis**: Groq LLM for product identification and specification extraction
4. **Image Search**: SerpAPI Bing search for professional product images
5. **Content Assembly**: Image downloading and caption formatting
6. **Delivery**: Multi-image Telegram post with technical specifications

### Node Flow
Telegram Photo → OCR → Text Processing → AI Analysis → Image Search → Download → Telegram Post


## 🚀 Setup Instructions

### Prerequisites

1. **n8n Account**: Self-hosted or cloud instance
2. **Telegram Bot**: Created via @BotFather
3. **API Keys**:
   - AWS Rekognition (for OCR)
   - Groq API (for LLM analysis)
   - SerpAPI (for Bing image search)
   - Telegram Bot Token

### Step-by-Step Configuration

#### 1. Telegram Bot Setup

1. Open Telegram and search for `@BotFather`
2. Create a new bot with `/newbot`
3. Save the bot token provided
4. Enable the bot to receive photos and messages
5. Start a conversation with your bot in Telegram

#### 2. AWS Rekognition Setup

1. Create an AWS account (free tier available)
2. Navigate to IAM and create a new user with `AmazonRekognitionFullAccess` policy
3. Generate access keys (Access Key ID and Secret Access Key)
4. Configure these in the "Analyze image1" node

#### 3. API Credentials Configuration

##### Groq API

1. Get API key from [console.groq.com](https://console.groq.com)
2. Configure in "Groq Chat Model1" node
3. Model used: `openai/gpt-oss-20b`

##### SerpAPI (Bing Image Search)

1. Sign up at [serpapi.com](https://serpapi.com)
2. Get your API key
3. Configure in "Bing_images search" node

##### Telegram Bot Token

Add your bot token to:

- "Telegram Trigger" node (for receiving messages)
- "Get a file" node
- All "Send a photo message" nodes
- "Send a text message" node

#### 3. Workflow Import

1. Copy the provided JSON
2. In n8n: Workflows → Import from JSON
3. Update all credentials in the relevant nodes

#### 4. Node Configuration Checklist

- [ ] Telegram Trigger: Add bot token and configure webhook
- [ ] AWS Rekognition: Add AWS credentials (Access Key ID and Secret Access Key)
- [ ] Groq Chat Model1: Add Groq API key
- [ ] SerpApi (Bing_images search): Add SerpAPI key
- [ ] All Telegram nodes: Verify bot token is correctly configured

## 📱 User Workflow

### How to Use the Bot

#### Start the Conversation

1. Open Telegram and find your bot
2. Send `/start` to begin

#### Upload Product Photo

1. Send a clear photo of a product with visible text
2. The photo should show labels, specifications, or branding

#### Wait for Processing

1. Bot will analyze the image (30-60 seconds)
2. Multiple processing steps occur automatically

#### Receive Results

1. Bot sends 3 professionally sourced product images
2. Detailed caption with brand, type, and specifications
3. All in a single, well-formatted post

### Example Use Cases

- **E-commerce sellers**: Create product listings from physical items
- **Retail employees**: Generate social media content from store products
- **Product reviewers**: Automate technical specification extraction
- **Social media managers**: Create professional product posts quickly

## 🔧 Customization Options

### Image Processing

Modify the "Extract Unique Texts" node to:

- Change text filtering logic
- Adjust minimum text length
- Modify deduplication rules
- Change substring filtering behavior

### Product Analysis

Adjust the AI prompt in "Basic LLM Chain" to:

- Change specification extraction criteria
- Modify brand detection logic
- Adjust number of specifications extracted
- Change response formatting

### Image Search

Modify "Parse Response" node to:

- Change search query construction
- Adjust image search terms
- Modify background preferences
- Change result prioritization

### Social Media Formatting

Customize "Format Caption" node to:

- Change caption structure
- Modify Markdown/formatting
- Adjust technical specification presentation
- Change branding emphasis

## 🛠️ Technical Details

### Nodes Used

- **n8n Core**: Telegram Trigger, Code, Merge, HTTP Request
- **AWS**: Rekognition (OCR)
- **LangChain**: ChainLlm, LmChatGroq
- **Community**: SerpApi (Bing search)

### Key Code Snippets

#### Image Text Extraction (`Extract Unique Texts` node)
// Processes AWS Rekognition output

// Deduplicates, filters, and sorts detected text

// Removes substrings to keep only meaningful phrases


#### Product Analysis (`Parse Response` node)
// Parses LLM output for brand, type, and specs

// Constructs optimized search query for product images

// Includes model numbers when available


#### Image Processing Pipeline (`Download Image` nodes)
// Downloads top 3 images from Bing search

// Uses separate HTTP requests for parallel downloading

// Handles errors gracefully with continueRegularOutput


## 🔒 Security & Best Practices

### API Security

1. **Use Environment Variables** for all API keys
2. **Rotate AWS credentials** regularly
3. **Monitor API usage** to avoid rate limits
4. **Use webhook secrets** for Telegram bot security

### Data Privacy

- User photos are processed through AWS Rekognition
- Extracted text is sent to Groq for analysis
- No user data is stored permanently in the workflow
- Consider GDPR compliance for EU users

### Error Handling

The workflow includes:

- Graceful error handling with `continueRegularOutput`
- Input validation for all processing steps
- Fallback behavior when images aren't found
- User-friendly error messages in Telegram

## 📊 Monitoring & Maintenance

### Success Indicators

- Successful photo upload and processing
- Relevant product images found and sent
- Accurate brand and specification extraction
- User satisfaction with generated posts

### Common Issues & Solutions

| Issue | Solution |
|-------|----------|
| No text detected | Improve photo quality, ensure text is visible |
| Wrong brand identified | Adjust LLM prompt for better brand detection |
| No images found | Modify search query construction |
| Telegram sending fails | Check bot token, verify chat permissions |
| AWS Rekognition errors | Check IAM permissions, verify region settings |

### Performance Optimization

1. **Image Size**: Telegram compresses images - request highest quality
2. **Parallel Processing**: Images download simultaneously
3. **Caching**: Consider caching frequently analyzed products
4. **Batching**: Process multiple images in sequence if needed

## 🚨 Limitations & Considerations

### Current Limitations

1. **Image Quality Dependency**: Requires clear, readable text
2. **Brand Recognition**: May not identify obscure brands
3. **Language Support**: Primarily English text recognition
4. **Image Availability**: Depends on Bing search results

### Ethical Considerations

- Respect copyright for sourced images
- Disclose automated content generation
- Ensure product claims are accurate
- Respect user privacy and data

### Cost Management

- AWS Rekognition: Pay-per-use pricing
- Groq API: Token-based pricing
- SerpAPI: Monthly subscription with usage limits
- Monitor usage to avoid unexpected costs

## 🤝 Support & Troubleshooting

### Getting Help

1. **n8n Community**: [community.n8n.io](https://community.n8n.io)
2. **Telegram Bot API**: [core.telegram.org/bots](https://core.telegram.org/bots)
3. **AWS Rekognition Docs**: AWS documentation
4. **Groq Support**: Developer documentation

### Debugging Tips

1. **Test Each Node**: Use n8n's test functionality
2. **Check Webhooks**: Ensure Telegram webhook is properly configured
3. **API Limits**: Monitor usage across all services
4. **User Permissions**: Verify all API credentials have correct permissions

## 📄 License & Compliance

Ensure compliance with:

- Telegram Bot Terms of Service
- AWS Service Terms
- Groq API Usage Policies
- SerpAPI Terms of Service
- Copyright laws for image usage

### Attribution Requirements

- Disclose automated content generation if required
- Credit image sources when applicable
- Comply with platform-specific automation rules

---

*Built with n8n - The extendable workflow automation tool.*  
*Perfect for e-commerce, retail, and social media management.*  
*Last Updated: 23/12/2025*
