# Liver Mitra Health Assistant

A lightweight, responsive, rule-based **liver-care chatbot widget** designed for the Liver Mitra website. It provides quick information about liver conditions, treatments, transplant support, appointments, contact details, and WhatsApp enquiries.

> **Medical disclaimer:** This assistant provides general information only. It is not a diagnosis tool or an emergency service.

## Features

- 💬 Floating chatbot button with tooltip
- 📱 Responsive desktop and mobile interface
- 🩺 Liver symptom guidance
- 📋 Liver disease, transplant, and surgery service menus
- 🫀 Liver transplant information
- 📅 Appointment enquiry form
- 🟢 WhatsApp integration with pre-filled messages
- 📞 Click-to-call contact support
- ⌨️ Free-text intent matching
- 🚨 Emergency keyword detection
- ✨ Typing animation and message timestamps
- ♿ Keyboard and ARIA support
- 🔒 No chat-history persistence; refresh starts a new conversation
- 🧼 User text escaping for safer HTML rendering

## Supported Topics

The chatbot includes predefined guidance for topics such as:

- Hepatitis A & E
- Hepatitis B
- Hepatitis C
- Fatty liver disease
- Cirrhosis / Chronic Liver Disease
- Liver cancer
- Liver diseases in children
- Living Donor Liver Transplant
- Deceased Donor Liver Transplant (DDLT)
- Split Liver Transplant
- Domino Liver Transplant
- Hepatectomy / Liver Resection
- Lobectomy
- Segmentectomy
- Wedge Resection
- Laparoscopic / Robotic Liver Surgery
- Liver injury
- Biliary / liver-related operations
- Jaundice and other common liver-related symptoms

## Tech Stack

- HTML5
- CSS3
- Vanilla JavaScript
- PHP for dynamic contact-number injection
- WhatsApp Click-to-Chat API

No JavaScript framework or external chatbot API is required.

## Project Structure

A typical integration can look like:

```text
project/
├── assets/
│   └── images/
│       ├── bot.png
│       └── fav-icon.svg
├── chatbot.php
└── ...
```

The supplied widget expects these image paths:

```text
assets/images/bot.png
assets/images/fav-icon.svg
```

Update the paths if your project uses a different directory structure.

## Installation

### 1. Add the widget

Place the chatbot code in your PHP page or save it as a reusable partial, for example:

```php
<?php include 'chatbot.php'; ?>
```

For best results, include it near the end of the page, before the closing `</body>` tag.

### 2. Provide the phone number

The widget currently reads the contact and WhatsApp number from PHP:

```php
const CONTACT_NUMBER = '<?= $phone ?>';
const WHATSAPP_NUMBER = '<?= $phone ?>';
```

Make sure `$phone` is defined before the chatbot is included:

```php
<?php
$phone = '+91XXXXXXXXXX';
?>
```

For WhatsApp, use a number that includes the country code. The script automatically removes spaces and other non-numeric characters when generating the `wa.me` link.

### 3. Add chatbot assets

Add your chatbot icon and Liver Mitra icon to:

```text
assets/images/bot.png
assets/images/fav-icon.svg
```

Or change the `src` attributes in the widget to match your asset paths.

## Usage

Click the floating chatbot button to open the assistant. Users can choose quick actions for:

```text
Book Appointment
Liver Symptoms
Treatments
Transplant
Contact
WhatsApp
```

Users can also type queries such as:

```text
fatty liver treatment
hepatitis b
liver transplant
jaundice
book appointment
contact
```

The chatbot normalizes the input and matches it against predefined intents and service names.

## Appointment Flow

The appointment form collects:

- Full name
- Phone number
- Liver-care concern
- Preferred consultation type
- Optional symptoms/message

After validation, the widget creates a pre-filled WhatsApp appointment request and opens WhatsApp in a new tab.

The request contains the patient's entered details, for example:

```text
New Liver Mitra Appointment Request

Name: [Name]
Phone: [Phone]
Concern: [Selected Concern]
Consultation: [Preferred Consultation]
Message: [Message]
```

The user must still send the prepared WhatsApp message to complete the enquiry.

## Emergency Handling

The assistant checks for selected emergency-related phrases such as:

```text
unconscious
vomiting blood
black stool
confusion
severe bleeding
difficulty breathing
```

When matched, it tells the user to seek immediate emergency medical care.

This keyword system is intentionally simple and **must not be treated as a complete emergency-detection system**.

## Customization

### Colors

The main theme is controlled through CSS variables:

```css
:root {
    --lm-primary: #0f766e;
    --lm-primary-2: #14b8a6;
    --lm-accent: #d99a35;
    --lm-dark: #082f36;
    --lm-bg: #f8fafc;
    --lm-border: #dbe4e8;
    --lm-text: #17202a;
    --lm-muted: #64748b;
}
```

Change these values to match your website branding.

### Services

Edit the `SERVICE_GROUPS` object to add, remove, or rename services:

```javascript
const SERVICE_GROUPS = {
    'Liver Diseases': [
        'Hepatitis B',
        'Hepatitis C',
        'Cirrhosis & CLD'
    ],
    'Liver Transplant': [
        'Living Donor Liver Transplant',
        'DDLT'
    ],
    'Liver Surgery': [
        'Hepatectomy (Liver Resection)',
        'Laparoscopic/Robotic Liver Surgery'
    ]
};
```

### Chatbot Responses

Free-text responses are controlled by the `intents` array. Each intent can contain keywords and either a predefined answer or an action.

Example:

```javascript
{
    keys: ['hepatitis b', 'hbv'],
    answer: `<b>Hepatitis B</b><br>Your response here.`
}
```

## Security & Privacy Notes

- Chat messages are not saved by this widget.
- Refreshing the page clears the current conversation.
- Appointment information is prepared locally and passed to WhatsApp when the user continues.
- User chat messages are inserted using `textContent`.
- Dynamic service names are escaped before being inserted into generated HTML.
- Keep medical responses reviewed and updated by qualified healthcare professionals.
- If you later connect this widget to a database or backend API, add appropriate server-side validation, authentication, rate limiting, CSRF protection, and privacy controls.

## Limitations

This is a **rule-based frontend assistant**, not an AI diagnostic system.

It does not:

- Diagnose medical conditions
- Replace a doctor or hepatologist
- Store chat history
- Automatically submit appointments to a database
- Confirm an appointment slot
- Provide real-time clinician availability
- Reliably detect every possible medical emergency
- Use an LLM or external AI API

## Browser Compatibility

The widget uses modern browser features including:

- `Object.values()`
- Template literals
- `Intl.DateTimeFormat`
- `requestAnimationFrame`
- `Element.classList`
- `window.open()`

It should work in current versions of Chrome, Edge, Firefox, Safari, and modern mobile browsers.

## Contributing

Contributions and improvements are welcome.

1. Fork the repository.
2. Create a feature branch.
3. Make your changes.
4. Test desktop and mobile behavior.
5. Submit a pull request.

For medical-content changes, ensure the information is reviewed before production deployment.

## License

No license is specified by the supplied source code.

If you plan to publish this as an open-source repository, add a `LICENSE` file and update this section with your chosen license.

## Disclaimer

The Liver Mitra Health Assistant is intended to provide general educational and navigation support. It should not be used for diagnosis, treatment decisions, or emergency assessment.

For urgent or severe symptoms, users should seek appropriate emergency medical care.
