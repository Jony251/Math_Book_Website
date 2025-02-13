# Visit Books

A modern web application built with Vue 3 and Vite for managing and organizing visits and bookings

## 🚀 Features

- Modern and responsive user interface
- Built with Vue 3 for optimal performance
- Fast development environment with Vite
- Component-based architecture
- CSS styling with modern best practices
- Contact form with EmailJS integration
- Form validation and error handling

## 📋 Prerequisites

- Node.js (v14 or higher)
- npm or yarn package manager
- EmailJS account for contact form functionality

## 🛠️ Installation

1. Clone the repository
2. Navigate to the project directory:
   ```bash
   cd visit_books
   ```
3. Install dependencies:
   ```bash
   npm install
   # or
   yarn install
   ```
4. Set up environment variables:
   - Copy `.env.example` to `.env`
   - Fill in your EmailJS credentials:
     ```
     VITE_EMAILJS_PUBLIC_KEY=your_public_key_here
     VITE_EMAILJS_TEMPLATE_ID=your_template_id_here
     VITE_EMAILJS_SERVICE_ID=your_service_id_here
     ```

## 📧 EmailJS Setup

1. Create an account at [EmailJS](https://www.emailjs.com/)
2. Create an Email Service (Gmail, Outlook, etc.)
3. Create an Email Template with the following variables:
   - `{{name}}` - Sender's name
   - `{{email}}` - Sender's email
   - `{{phone}}` - Sender's phone number
   - `{{date}}` - Submission date
   - `{{message}}` - The formatted message
4. Get your credentials:
   - Public Key (Account > API Keys)
   - Template ID (Email Templates > Your Template)
   - Service ID (Email Services > Your Service)

## 🏃‍♂️ Development

To start the development server:

```bash
npm run dev
# or
yarn dev
```

The application will be available at `http://localhost:5173`

## 🚀 Deployment

### Environment Variables

When deploying to production, you need to set up environment variables:

1. **Netlify**:
   - Navigate to Site settings > Build & deploy > Environment variables
   - Add each variable from your .env file

2. **Vercel**:
   - Go to Project settings > Environment Variables
   - Add each variable separately

3. **Traditional hosting**:
   - Upload the `.env` file to your server
   - Ensure it's in the root directory
   - Verify the file is not publicly accessible

## 🏗️ Project Structure

```
visit_books/
├── public/           # Static assets
├── src/             # Source files
│   ├── components/  # Vue components
│   │   ├── contact/ # Contact form component
│   │   └── ...
│   ├── App.vue      # Main application component
│   └── base.css     # Global CSS styles
├── .env.example     # Example environment variables
├── .gitignore       # Git ignore rules
└── README.md        # Project documentation
```

## 📝 Environment Variables

The following environment variables are required:

| Variable | Description |
|----------|-------------|
| `VITE_EMAILJS_PUBLIC_KEY` | Your EmailJS public key |
| `VITE_EMAILJS_TEMPLATE_ID` | Your EmailJS template ID |
| `VITE_EMAILJS_SERVICE_ID` | Your EmailJS service ID |

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.
