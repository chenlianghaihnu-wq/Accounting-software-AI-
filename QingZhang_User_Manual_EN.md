# QingZhang Software User Manual

Version: 1.0.0  
Developer: CHENLH  
Supported Platform: Android 8.0 and above  
Positioning: A local-first personal intelligent bookkeeping tool

## 1. Software Overview

QingZhang is a bookkeeping application designed for personal daily use. Its core goal is to help you complete bookkeeping with as few operations as possible. You can enter a natural-language sentence, such as “I had beef noodles for lunch today, 23”, or manually fill in the amount, major category, subcategory, and notes. You can also recognize receipts from photos, or import CSV, JSON, XLSX, images, or full text.

By default, the software stores data in the local database on your phone. If you have not actively configured a cloud model or OCR service, ordinary bookkeeping, transaction viewing, statistics, budgeting, and rule management are all completed locally on the device. When cloud text models, receipt-structuring models, Baidu OCR, or similar functions are involved, the program will send the text or image content you actively submit to the services you have configured.

## 2. Installation and First Use

### 2.1 Installing the APK

After sending `app-release.apk` to your phone, tap it in the phone’s file manager to install it. If the system prompts that installation from unknown sources is not allowed, you need to allow the current file manager or browser to install apps from unknown sources in the system settings.

### 2.2 About Overwrite Installation

Android requires that the signature remain the same when upgrading an app with the same package name. If you previously installed an unsigned test version or a debug version, the officially signed version may not be able to overwrite it directly. In this case, you need to uninstall the old version first and then install the new version. Uninstalling will clear the local bill data on that phone, so please export or back up your data first.

If the previously installed version uses the same CHENLH signature, the new version can be installed over it while keeping the old database.

### 2.3 First-Launch Declaration

When you open the software for the first time, a developer declaration will be displayed. You need to tap “Agree and Use” to enter the software. If you tap “Disagree and Exit”, the program will close directly.

The declaration can be viewed again from the `⋮` menu in the upper-right corner of the “Me” page.

## 3. Home Page

The Home page is the most commonly used bookkeeping entry point. It includes quick bookkeeping, manual bookkeeping, receipt recognition, and a recent-bill display.

### 3.1 One-Sentence Bookkeeping

Enter bill text in the input box on the Home page, then tap “Recognize and Save Bill”.

Examples:

```text
I had beef noodles for lunch today, 23
Taxi yesterday 18.5
Salary received 5000
Milk tea 12, bus 2, dinner 36
```

The program will automatically recognize the amount, type, major category, subcategory, expense item, and time, and then save the result to the bill database.

If a paragraph contains multiple amounts, the program will try to split it into multiple bills. For example:

```text
Breakfast 8, bus 2, lunch 23
```

This will usually generate three records.

### 3.2 Manual Bookkeeping When the Input Is Empty

If the input box on the Home page is empty, tapping “Recognize and Save Bill” will no longer show an error. Instead, it will open the “Manual Bookkeeping” window.

Manual bookkeeping allows you to fill in:

- Type: expense, income, or transfer.
- Amount: required, such as `23` or `23.5`.
- Major category: such as dining, transportation, shopping, income, or other.
- Subcategory: optional; selected from the existing subcategories under the current major category.
- Expense item / matter: such as beef noodles, bus, or salary.
- Notes: optional.
- Tags: optional; separated by commas or Chinese enumeration commas.
- Time: optional; supports formats such as `2026-05-02`, `2026-05-02 18:30`, and `2026/05/02 18:30`.

The amount is required. If no time is entered, the current time is used by default.

Major categories and subcategories in manual bookkeeping are selected through a multi-line tap interface. After selecting expense, income, or transfer, the major-category area directly displays the available major categories. After tapping a major category, the subcategory area refreshes to show the subcategories under that major category. Tap again to select one.

### 3.3 Receipt Photo Recognition and Entry

Tap “Recognize Receipt Photo and Enter Bill” to choose between taking a photo or selecting an image from the album.

The recognition process is:

1. The image is first sent to Baidu OCR and recognized as plain text.
2. The OCR text is then sent to the “receipt-structuring model”.
3. The receipt-structuring model generates multiple bills by product or service detail.
4. The program saves the generated bills.

Before using this function, you need to enter the Baidu OCR API Key and Secret Key, as well as the API Key, Base URL, and model name of the receipt-structuring model in “Model Configuration”.

### 3.4 Home Bill List

The Home page displays recent bills by date. Each date header shows text such as “April 28, Tuesday”, with the year displayed beside it in smaller light-colored text.

Each bill row displays a major-category color block on the left and the amount on the right. The middle area shows the expense item, subcategory, and major category. The display rules are roughly as follows:

- If both expense item and subcategory exist: expense item · subcategory · major category.
- If expense item exists but subcategory does not: expense item · major category.
- If only subcategory exists: subcategory · major category.
- If only major category exists: major category.

If a bill has a refund, the refund amount is shown below the total amount in a smaller font. The actual statistical amount is calculated as “total amount - refund amount”.

### 3.5 Editing, Refunds, and Deletion

Tap a bill to enter the edit window.

Editable content includes:

- Total amount.
- Category.
- Notes.
- Tags.
- Refund.

Tap “Refund” to enter a refund amount, or tap “Full Refund”. Bills with refunds are calculated by actual amount in statistics and budgets.

Long-press a bill to enter multi-select deletion mode. The long-pressed bill is selected by default, and you can then tap or swipe to select multiple records. The bottom bar displays “selected count”, Delete, and Cancel buttons.

Deletion is soft deletion. Records are moved to “Recently Deleted” instead of being permanently deleted immediately.

## 4. Transactions Page

The Transactions page is used to view and search all bills.

### 4.1 Viewing Transactions

The Transactions page displays bills grouped by date, using the same display rules as the Home page. Data on the Home page and the Transactions page are synchronized: additions, deletions, or recoveries on one side are also updated on the other.

### 4.2 Searching Bills

You can search bills at the top of the Transactions page. Both ordinary keywords and natural-language queries with conditions are supported.

Examples:

```text
Beef noodles
Dining this month
Expenses yesterday
Shopping over 100
Transportation last month
```

Search will try to match bill titles, notes, categories, tags, time, and amount conditions.

### 4.3 Deletion and Recovery

The Transactions page also supports long-pressing to enter multi-select deletion mode. Deleted records are moved to “Recently Deleted”.

## 5. Statistics Page

The Statistics page includes monthly reports, weekly reports, and yearly reports.

### 5.1 Monthly Report

The monthly report displays data such as current-month income, expenses, balance, and average daily spending.

There is a small calendar in the monthly report:

- The first row shows Monday to Sunday.
- Each date shows that day’s spending below it.
- The left side of each row shows the spending for that week.
- Tapping a day opens a pop-up window showing brief bills for that date.

Year and month can be selected below. Tapping the year expands the year selector, and months are displayed in multiple rows. The currently selected month has a special style.

### 5.2 Weekly Report

The weekly report calculates income, expenses, balance, category share, and trends for the current week.

### 5.3 Yearly Report

The yearly report calculates total income, total expenses, balance, and category structure for the current year.

### 5.4 Charts and Rankings

The Statistics page includes:

- Daily trend chart.
- Category share chart.
- Spending ranking.
- Abnormal spending reminders.

Refunded bills participate in statistics by actual amount, meaning total amount minus refund amount.

## 6. Budget Page

The Budget page is used to set and view the current month’s budget.

### 6.1 Adding the Total Budget for the Current Month

Enter the budget amount and save it. By default, the budget applies to the current calendar month.

### 6.2 Viewing Budget Progress

Budget progress displays:

- Current amount used.
- Total budget.
- Usage percentage.
- Status: normal, close to limit, or overspent.

Bills after refunds are counted in the budget by actual amount.

## 7. Me Page

The “Me” page includes the app name, data import/export, large-model bill checking, recognition rules, subscription management, Recently Deleted, and other functions.

### 7.1 Developer Information

Tap the `⋮` menu in the upper-right corner to view the developer declaration.

The main content includes:

- Developer: CHENLH.
- The software is independently developed, for personal use and free sharing.
- The software is provided as is and does not constitute financial, tax, legal, investment, or consumption advice.
- Bill data is stored locally by default, and the app does not connect to the network by default. Local rule recognition and manual bookkeeping can both be used offline.
- When the Home input box is empty, tapping “Recognize and Save Bill” opens the manual bookkeeping interface.
- Baidu OCR, DeepSeek, and other cloud models are configured by the user and serve as extended network channels of the software. The network, privacy, and cost risks caused by uploading relevant text, images, or recognition content to model service providers are borne by the user.
- During developer testing, Baidu OCR and DeepSeek V4 Flash were used. A local Qwen 3-0.6B model was also tested, but it ran slowly on mobile devices. Users may configure other compatible models on their own. Model quotas, prices, speeds, and service stability are subject to the actual rules of the service providers. The software does not include the developer’s API Key and does not collect model fees on behalf of any provider.
- The software is free to use and share, but all rights are reserved.
- Links to Bilibili, Xiaohongshu, and Douyin homepages.

### 7.2 App Name

You can customize the display name inside the app. This name mainly affects the title shown inside the software and may not change the app name displayed under the system desktop icon.

### 7.3 Exporting CSV

Tap “Export CSV” to export the current bill data.

CSV fields include:

- Consumption time.
- Creation time.
- Type.
- Amount.
- Refund.
- Actual amount.
- Category.
- Notes.
- Tags.
- Account.
- Source.
- Original input.

The exported file is saved in the `exports` folder under the app’s external file directory.

### 7.4 Importing Data

Tap “Import Data” to display multiple import methods.

#### Import CSV Export Format

This is used to import CSV files exported by this software. It is suitable for recovery from an old phone or backup file.

#### Import JSON Backup Format

This is used to import JSON backups created by this software.

#### Text Import

After tapping this option, a text box appears directly. Paste a section of bill text into it, and the program sends the text to the “receipt-structuring model” to generate structured bills.

This is suitable for importing chat records, travel expense lists, manually organized spending details, and similar content.

#### CSV / XLSX to Text Import

After selecting a CSV or XLSX file, the program first converts the table content into plain text locally on the phone.

CSV-to-text conversion method:

- First parse commas, line breaks, and quotation marks.
- Each row is preserved as one line.
- Each column is separated by a tab.

XLSX-to-text conversion method:

- The program reads the XLSX file as a zip file.
- It extracts `xl/sharedStrings.xml` and table XML files under `xl/worksheets/`.
- It parses cell text.
- Cells are separated by tabs, and rows are separated by line breaks.

The converted plain text is then sent to the “receipt-structuring model” to generate bills.

#### Image Import Receipt Image Recognition

After selecting an image, the program uses the receipt image recognition process:

1. The image is sent to Baidu OCR.
2. OCR returns plain text.
3. The plain text is sent to the receipt-structuring model.
4. Bills are generated and saved.

### 7.5 Large-Model Bill Checking

Large-model bill checking is used to check whether the categories of existing bills are reasonable.

You can choose:

- Check bills added since the last check.
- Check by date range.

After tapping, the software first displays the bills to be checked. After confirmation, they are sent to the receipt-structuring model. Progress is displayed during the checking process.

After the model returns suggestions, the program opens a review window showing the before-and-after content of each suggestion. You can choose whether to accept each suggestion one by one.

After accepting suggestions:

- The program modifies the corresponding bills.
- If new major categories, subcategories, or expense items appear, they will be added to the recognition rules after your confirmation.
- Similar inputs in the future will be easier to recognize correctly.

### 7.6 Opening the Export Folder

You can view exported CSV, TXT, or JSON files and try to open or share them.

If the system file manager cannot directly enter the app-specific directory, you can open or share files directly from this interface.

### 7.7 Manual JSON Backup

Tapping this option generates a JSON backup file of the current data. It is recommended to back up before uninstalling the app, changing phones, or installing a version with a different signature.

### 7.8 Recently Deleted

Recently Deleted works like a recycle bin.

Available operations include:

- Restore a single item.
- Permanently delete a single item.
- Restore multiple selected items.
- Permanently delete multiple selected items.
- Empty the recycle bin.

The recycle bin automatically cleans records deleted more than one month ago.

## 8. Recognition Rules

Recognition rules help the program recognize text as the correct major category, subcategory, and expense item.

### 8.1 Major Categories, Subcategories, and Expense Items

The software uses a three-level structure:

- Major category: dining, transportation, shopping, income, etc.
- Subcategory: lunch, breakfast, bus, subway, etc.
- Expense item: beef noodles, coffee, bus ride, hotel, etc.

During recognition, as long as any major category, subcategory, or expense item can be matched, the program will try to categorize the bill. Only when it cannot be recognized at all will it fall back to “Other”.

### 8.2 Adding Major Categories

You can add major categories in the “Recognition Lexicon”. Multiple names can be entered at once, separated by commas, Chinese enumeration commas, or line breaks.

### 8.3 Adding Subcategories

After selecting a major category, you can add subcategories. Multiple subcategories can also be added at once.

Example:

```text
Lunch, dinner, late-night snack
```

### 8.4 Adding Expense Items

You can select a major category, or select a subcategory under that major category, and then add expense items.

Expense items also support batch input:

```text
Beef noodles, claypot rice, malatang
```

After being added, they are immediately synchronized to the recognition rules. Manually added expense items have higher priority and will participate in recognition first.

### 8.5 Deleting Rules

Rules can be deleted by level: major category, subcategory, or expense item.

Deletion restrictions:

- A subcategory can be deleted only when the number of expense items under it is 0.
- A major category can be deleted only when the number of subcategories under it is 0.
- When deleting an expense item, the subcategory is optional. If a subcategory is selected, only expense items under that subcategory can be deleted.

### 8.6 Viewing All Rules

Tap “View All Rules” to enter the rule overview page.

The rule overview page displays all major categories. After tapping a major category, all subcategories and expense items under that category are displayed below.

Here you can:

- Directly edit expense item text.
- Delete expense items.
- Add expense items.
- Long-press a subcategory to delete it.
- Save all changes together through “Confirm Changes”.

Before changes are saved, a confirmation window shows the modified content. The changes take effect only after confirmation.

### 8.7 Structured Batch Rule Addition

The bottom of the View All Rules page supports structured batch addition.

Format example:

```text
(Dining), (Lunch), (Beef noodles, rice bowl, fried rice)
(Transportation), (Bus), (Bus ride, bus)
(Shopping), (), (Tissues, laundry detergent)
```

Rules:

- Major category is required.
- Subcategory may be filled in or left blank.
- Expense items may be filled in or left blank.
- Multiple expense items are separated by commas.

### 8.8 Strong Constraint Rules

Strong constraint rules are used to handle words that are easy to confuse but have a clear direction.

Examples:

- “Eat” is usually strongly bound to dining.
- “Drink” is usually strongly bound to dining.
- “High-speed rail” is strongly bound to transportation.

Strong constraint rules are separated from ordinary expense-item rules and can be added or deleted independently. They are used to resolve ambiguities such as when “mian” may mean beef noodles or a facial mask.

## 9. Model Configuration

Tap “Model Configuration” in the upper-right corner of the Home page to enter the model deployment and selection interface.

### 9.1 Text Bookkeeping Model

The text bookkeeping model has three channels:

- Local rules: uses only local rule recognition.
- Local model: uses a local model on the phone.
- Cloud model: uses a cloud text model.

Configurations take effect only after tapping Save in the upper-right corner. If you only switch the button without saving, the next time you enter the page it will still show the currently effective channel.

### 9.2 API Key Privacy Display

API Keys are hidden by black dots by default. Tap the eye icon on the right to show or hide them again. Each time you re-enter the Model Configuration page, API Keys are hidden by default.

### 9.3 Local Model

You can import a local text model. After import, the program will try to initialize the local model. Availability depends on the phone’s performance, model format, and runtime environment.

### 9.4 Cloud Text Model

You need to fill in:

- Base URL.
- API Key.
- Model name.

The cloud text model is used for the “cloud model” channel of Home-page text bookkeeping.

### 9.5 Receipt Image Recognition

You need to fill in:

- Baidu OCR API Key.
- Baidu OCR Secret / Service Key.
- Baidu OCR Endpoint.

Image recognition first calls Baidu OCR to convert the image into plain text.

### 9.6 Receipt-Structuring Model

You need to fill in:

- Base URL.
- API Key.
- Model name.

The receipt-structuring model is used for:

- Structured organization after receipt image recognition.
- Text import.
- CSV / XLSX to text import.
- Image import.
- Large-model bill checking.

# Configuration Tutorial

## Receipt-Structuring Model

Website: https://platform.deepseek.com/sign_in

After logging in, top up 10 RMB. Topping up 1 RMB is also acceptable.

Then go to the API Key page.

Click Create API Key, enter any name you like, and then an API Key will be generated. Note that this key is shown only once when it is created, so copy it and save it to your phone. Paste the API Key into the receipt-structuring model section of the program to complete deployment.

## OCR Recognition Model

Website: Baidu AI Cloud login page: https://login.bce.baidu.com/?_=1777713221929&redirect=https%3A%2F%2Fconsole.bce.baidu.com%2Fai-engine%2Focr%2Foverview%2Findex

Register, log in, and complete personal verification.

On the relevant page, click Create Application and fill in the required information. There are no special requirements.

After creation, a new application can be seen in the application list. Copy the API Key and Secret Key into the receipt image recognition section of the program’s model deployment page to complete deployment.

## 10. Home Screen Widget

The software includes a quick-entry home screen widget.

After adding it to the home screen, tapping the widget opens a small window. Enter bill information and tap “Enter”. The program automatically recognizes and saves it, then returns to the home screen after success. Tapping “Cancel” also returns to the home screen.

The home screen widget is suitable for temporary quick records, such as:

```text
Breakfast 8
Taxi 19
Coffee 16
```

## 11. Data Security and Backup Suggestions

### 11.1 Local Database

Bills are saved in the local database on the phone by default. Changing phones, uninstalling the app, or clearing app data will affect local bills.

### 11.2 Regular Export

It is recommended to regularly use:

- Export CSV.
- Manual JSON backup.

CSV is suitable for viewing and migration, while JSON is more suitable for complete backups.

### 11.3 Cloud Model Risks

The app does not connect to the network by default. Basic functions such as local rule bookkeeping, manual bookkeeping, transactions, statistics, budgeting, and rule management can all be used offline. Only when you actively configure and use Baidu OCR, DeepSeek, or other cloud models will the software send relevant text, table content, or image recognition content to the service address you configured. Please do not upload sensitive information that you do not want third-party services to process.

## 12. Frequently Asked Questions

### 12.1 Why does the new version say it cannot overwrite the old version?

This is usually due to different signatures. Debug versions, unsigned versions, and the officially signed CHENLH version cannot directly overwrite one another. You need to uninstall the old version first and then install the new version. Please back up before uninstalling.

### 12.2 Why was my one-sentence input recognized incorrectly?

The rule library may not contain the corresponding expense item, or the keyword may be ambiguous. You can go to “Me - Recognition Lexicon” to add expense items, subcategories, or strong constraint rules.

### 12.3 Why does image import say that model configuration is required?

Image import requires two configurations: Baidu OCR and the receipt-structuring model. Both are required.

### 12.4 Why does text import also require the receipt-structuring model?

Text import, CSV/XLSX to text import, and image import all eventually send plain text to the “receipt-structuring model”, which generates structured bills.

### 12.5 Why do statistics decrease after a refund?

This is normal behavior. The bill total amount is used for display, while the actual amount equals total amount minus refund amount. Statistics, budgets, and amount-based searches prioritize the actual amount.

### 12.6 Will Recently Deleted be kept forever?

No. Recently Deleted automatically clears records deleted more than one month ago.

### 12.7 Is the software paid?

The current version is for personal use and free sharing. Cloud models, OCR, or third-party services may charge fees through their respective service providers, and users should confirm the cost and availability themselves.

## 13. Release Statement Summary

This software is independently developed by CHENLH and shared free of charge. The software is provided as is and does not constitute financial, tax, legal, investment, or consumption advice. Unless explicitly authorized by the developer, this software, its name, interface, rule library, model prompts, or derivative versions may not be used for commercial sale, malicious distribution, infringement, or misleading promotion. The developer reserves all rights.
