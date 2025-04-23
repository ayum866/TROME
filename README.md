<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Search Engine</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        h1{
            color: blue;
            padding: 10px;
        }
        h3{
            color:black;
        }
    </style>
</head>
<h1><b>ŢŘɸɰɞ</b></h1>   
<h3>Powered By-TWINxBROTHERS</h3>
<body class="bg-gray-100 flex flex-col items-center justify-start min-h-screen py-10">                    
    <button id="google-signin">Sign in with Google</button>
    <div class="bg-white rounded-full shadow-md w-full max-w-md p-4 mb-8 flex items-center">
        <input
            type="text"
            id="searchBar"
            placeholder="Search for websites..."
            class="flex-grow focus:outline-none px-4"
        />
        <button id="searchButton" class="bg-blue-500 hover:bg-blue-600 text-white rounded-full p-2">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-search"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.3-4.3"/></svg>
        </button>
    </div>

  <div id="resultsContainer" class="w-full max-w-md">
        </div>
  <script>
        const websiteData = [
            { name: "Google", url: "https://www.google.com", keywords: ["search", "google", "find", "information"] },
            { name: "YouTube", url: "https://www.youtube.com", keywords: ["videos", "youtube", "watch", "entertainment"] },
            { name: "Amazon", url: "https://www.amazon.com", keywords: ["shopping", "amazon", "buy", "products"] },
            { name: "Facebook", url: "https://www.facebook.com", keywords: ["social", "facebook", "connect", "friends"] },
            { name: "Wikipedia", url: "https://www.wikipedia.org", keywords: ["information", "wikipedia", "encyclopedia", "knowledge"] },
            { name: "Twitter", url: "https://www.twitter.com", keywords: ["social", "twitter", "news", "updates"] },
            { name: "Instagram", url: "https://www.instagram.com", keywords: ["social", "instagram", "photos", "videos"] },
            { name: "LinkedIn", url: "https://www.linkedin.com", keywords: ["professional", "linkedin", "jobs", "networking"] },
            { name: "Reddit", url: "https://www.reddit.com", keywords: ["social", "reddit", "forums", "community"] },
            { name: "Netflix", url: "https://www.netflix.com", keywords: ["streaming", "netflix", "movies", "tv shows"] },
            { name: "Microsoft", url: "https://www.microsoft.com", keywords: ["software", "microsoft", "windows", "office"] },
            { name: "Apple", url: "https://www.apple.com", keywords: ["technology", "apple", "iphone", "mac"] },
            { name: "Yahoo", url: "https://www.yahoo.com", keywords: ["news", "yahoo", "mail", "search"] },
            { name: "eBay", url: "https://www.ebay.com", keywords: ["shopping", "ebay", "buy", "sell"] },
            { name: "PayPal", url: "https://www.paypal.com", keywords: ["finance", "paypal", "money", "payments"] },
            { name: "CNN", url: "https://www.cnn.com", keywords: ["news", "cnn", "world", "breaking"] },
            { name: "BBC", url: "https://www.bbc.com", keywords: ["news", "bbc", "uk", "international"] },
            { name: "The New York Times", url: "https://www.nytimes.com", keywords: ["news", "nytimes", "usa", "world"] },
            { name: "The Washington Post", url: "https://www.washingtonpost.com", keywords: ["news", "washington post", "politics", "national"] },
            { name: "ESPN", url: "https://www.espn.com", keywords: ["sports", "espn", "scores", "news"] },
            { name: " சுகாதார அமைச்சகம்", url: "https://mohfw.gov.in/", keywords: ["Ministry of Health and Family Welfare", "Indian Health Ministry", "Covid-19", "Health"] },
            { name: "ISRO", url: "https://www.isro.gov.in/", keywords: ["Indian Space Research Organisation", "Space", "India", "Science"] },
            { name: "DRDO", url: "https://www.drdo.gov.in/", keywords: ["Defence Research and Development Organisation", "Military", "Research", "India"] },
            { name: "வருமான வரித் துறை", url: "https://www.incometax.gov.in/", keywords: ["Income Tax Department", "Tax", "India", "Finance"] },
            { name: "இந்திய ரயில்வே", url: "https://indianrailways.gov.in/", keywords: ["Indian Railways", "Railways", "Travel", "India"] },
            { name: "Aadhaar", url: "https://uidai.gov.in/", keywords: ["Aadhaar", "UIDAI", "India", "Identity"] },
            { name: "UGC", url: "https://www.ugc.ac.in/", keywords: ["University Grants Commission", "Education", "India", "Universities"] },
            { name: "AICTE", url: "https://www.aicte-india.org/", keywords: ["All India Council for Technical Education", "Engineering", "Technical Education", "India"] },
            { name: "NCERT", url: "https://ncert.nic.in/", keywords: ["National Council of Educational Research and Training", "Education", "Books", "India"] },
            { name: "CBSE", url: "https://www.cbse.gov.in/", keywords: ["Central Board of Secondary Education", "Education", "Schools", "India"] },
            { name: "ஜிமெயில்", url: "https://mail.google.com/", keywords: ["Gmail", "Email", "Google", "Communication"] },
            { name: "கூகிள் மேப்ஸ்", url: "https://www.google.com/maps", keywords: ["Google Maps", "Maps", "Navigation", "Travel"] },
            { name: "கூகிள் டிரைவ்", url: "https://www.google.com/drive/", keywords: ["Google Drive", "Storage", "Cloud", "Files"] },
            { name: "மைக்ரோசாஃப்ட் 365", url: "https://www.microsoft365.com/", keywords: ["Microsoft 365", "Office", "Word", "Excel"] },
             { name: "ஆப்பிள் ஐகிளவுட்", url: "https://www.icloud.com/", keywords: ["iCloud", "Apple", "Storage", "Cloud"] },
            { name: "டிராப்பாக்ஸ்", url: "https://www.dropbox.com/", keywords: ["Dropbox", "Storage", "Files", "Cloud"] },
            { name: "அடோப் கிரியேட்டிவ் கிளவுட்", url: "https://www.adobe.com/", keywords: ["Adobe Creative Cloud", "Photoshop", "Illustrator", "Design"] },
            { name: "பிளாக்ஸ்பாட்", url: "https://www.blogger.com/", keywords: ["Blogger", "Blog", "Publishing", "Writing"] },
            { name: "வேர்ட்பிரஸ்", url: "https://wordpress.com/", keywords: ["WordPress", "Blog", "Website", "Publishing"] },
            { name: "ஜூம்", url: "https://zoom.us/", keywords: ["Zoom", "Meetings", "Video Conference", "Communication"] },
            { name: "ஸ்கைப்", url: "https://www.skype.com/", keywords: ["Skype", "Communication", "Video Call", "Chat"] },
            { name: "மைக்ரோசாஃப்ட் டீம்ஸ்", url: "https://www.microsoft.com/en-in/microsoft-teams/group-chat-software", keywords: ["Microsoft Teams", "Collaboration", "Meetings", "Chat"] },
            { name: "ஸ்லாக்", url: "https://slack.com/", keywords: ["Slack", "Communication", "Team", "Collaboration"] },
            { name: "ட்ரீலோ", url: "https://trello.com/", keywords: ["Trello", "Project Management", "Kanban", "Productivity"] },
            { name: "அசானா", url: "https://asana.com/", keywords: ["Asana", "Project Management", "Tasks", "Collaboration"] },
            { name: "github", url: "https://github.com/", keywords: ["GitHub", "Code", "Version Control", "Development"] },
            { name: "ஸ்டாக் ஓவர்ஃப்ளோ", url: "https://stackoverflow.com/", keywords: ["Stack Overflow", "Programming", "Questions", "Answers"] },
            { name: "மோசிலா பயர்பாக்ஸ்", url: "https://www.mozilla.org/", keywords: ["Mozilla Firefox", "Browser", "Internet", "Web"] },
            { name: "சஃபாரி", url: "https://www.apple.com/safari/", keywords: ["Safari", "Browser", "Apple", "Web"] },
            { name: "ஒபேரா", url: "https://www.opera.com/", keywords: ["Opera", "Browser", "Internet", "Fast"] },
            { name: "விக்கிப்பீடியா", url: "https://en.wikipedia.org/wiki/Main_Page", keywords: ["Wikipedia", "Encyclopedia", "Information", "Knowledge"] },
            { name: "பிரிட்டானிக்கா", url: "https://www.britannica.com/", keywords: ["Britannica", "Encyclopedia", "Information", "Education"] },
            { name: "வெப்எம்டி", url: "https://www.webmd.com/", keywords: ["WebMD", "Health", "Medical", "Information"] },
            { name: "Mayo Clinic", url: "https://www.mayoclinic.org/", keywords: ["Mayo Clinic", "Health", "Medical", "Hospital"] },
            { name: "NIH", url: "https://www.nih.gov/", keywords: ["NIH", "National Institutes of Health", "Research", "Health"] },
            { name: "CDC", url: "https://www.cdc.gov/", keywords: ["CDC", "Centers for Disease Control", "Health", "Prevention"] },
            { name: "வெதர் சேனல்", url: "https://weather.com/", keywords: ["Weather Channel", "Weather", "Forecast", "Climate"] },
            { name: "AccuWeather", url: "https://www.accuweather.com/", keywords: ["AccuWeather", "Weather", "Forecast", "Temperature"] },
            { name: "Google News", url: "https://news.google.com/", keywords: ["Google News", "News", "Current Events", "World"] },
            { name: "ஏபிசி நியூஸ்", url: "https://abcnews.go.com/", keywords: ["ABC News", "News", "Politics", "US"] },
            { name: "சிபிஎஸ் நியூஸ்", url: "https://www.cbsnews.com/", keywords: ["CBS News", "News", "National", "World"] },
            { name: "பாக்ஸ் நியூஸ்", url: "https://www.foxnews.com/", keywords: ["Fox News", "News", "Politics", "Opinion"] },
            { name: "ராய்ட்டர்ஸ்", url: "https://www.reuters.com/", keywords: ["Reuters", "News", "International", "Business"] },
            { name: "அசோசியேட்டட் பிரஸ்", url: "https://apnews.com/", keywords: ["Associated Press", "AP", "News", "Global"] },
            { name: "பிபிசி ஸ்போர்ட்ஸ்", url: "https://www.bbc.com/sport", keywords: ["BBC Sports", "Sports", "Football", "Cricket"] },
            { name: "ESPN", url: "https://www.espn.com/", keywords: ["ESPN", "Sports", "Scores", "News"] },
            { name: "யாஹூ ஸ்போர்ட்ஸ்", url: "https://sports.yahoo.com/", keywords: ["Yahoo Sports", "Sports", "News", "Scores"] },
            { name: "என்.பி.ஏ.", url: "https://www.nba.com/", keywords: ["NBA", "Basketball", "Scores", "News"] },
            { name: "எம்.எல்.பி.", url: "https://www.mlb.com/", keywords: ["MLB", "Baseball", "Scores", "News"] },
            { name: "என்.எப்.எல்.", url: "https://www.nfl.com/", keywords: ["NFL", "Football", "Scores", "News"] },
            { name: "ஐ.எம்.டி.பி.", url: "https://www.imdb.com/", keywords: ["IMDb", "Movies", "Films", "Reviews"] },
            { name: "ராட்டன் டொமேட்டோஸ்", url: "https://www.rottentomatoes.com/", keywords: ["Rotten Tomatoes", "Movies", "Reviews", "Critics"] },
            { name: "மெடாகிரிடிக்", url: "https://www.metacritic.com/", keywords: ["Metacritic", "Movies", "Reviews", "Games"] },
            { name: "பாகஸ் ஆபிஸ் மோஜோ", url: "https://www.boxofficemojo.com/", keywords: ["Box Office Mojo", "Movies", "票房", "Industry"] },
            { name: "சவுண்ட் கிளவுட்", url: "https://soundcloud.com/", keywords: ["SoundCloud", "Music", "Audio", "Artists"] },
            { name: "ஸ்பாடிஃபை", url: "https://www.spotify.com/", keywords: ["Spotify", "Music", "Streaming", "Songs"] },
            { name: "Pandora", url: "https://www.pandora.com/", keywords: ["Pandora", "Music", "Radio", "Streaming"] },
            { name: "Apple Music", url: "https://www.apple.com/apple-music/", keywords: ["Apple Music", "Music", "Streaming", "Songs"] },
            { name: "அமேசான் மியூசிக்", url: "https://music.amazon.com/", keywords: ["Amazon Music", "Music", "Streaming", "Songs"] },
            { name: "Etsy", url: "https://www.etsy.com/", keywords: ["Etsy", "Shopping", "Handmade", "Crafts"] },
            { name: "Walmart", url: "https://www.walmart.com/", keywords: ["Walmart", "Shopping", "Retail", "Deals"] },
            { name: "Target", url: "https://www.target.com/", keywords: ["Target", "Shopping", "Retail", "Deals"] },
            { name: "Best Buy", url: "https://www.bestbuy.com/", keywords: ["Best Buy", "Electronics", "Shopping", "Tech"] },
            { name: "Home Depot", url: "https://www.homedepot.com/", keywords: ["Home Depot", "Home Improvement", "Shopping", "DIY"] },
            { name: "Lowes", url: "https://www.lowes.com/", keywords: ["Lowes", "Home Improvement", "Shopping", "DIY"] },
            { name: "வேஃபேர்", url: "https://www.wayfair.com/", keywords: ["Wayfair", "Furniture", "Home Decor", "Shopping"] },
            { name: "Overstock", url: "https://www.overstock.com/", keywords: ["Overstock", "Furniture", "Home Goods", "Shopping"] },
            { name: "சீயர்ஸ்", url: "https://www.sears.com/", keywords: ["Sears", "Shopping", "Appliances", "Tools"] },
            { name: "Kohl's", url: "https://www.kohls.com/", keywords: ["Kohl's", "Shopping", "Clothing", "Home Goods"] },
             { name: "ஸ்டார்பக்ஸ்", url: "https://www.starbucks.com/", keywords: ["Starbucks", "Coffee", "Drinks", "Food"] },
            { name: "மெக்டொனால்ட்ஸ்", url: "https://www.mcdonalds.com/", keywords: ["McDonald's", "Fast Food", "Burgers", "Fries"] },
            { name: "சப்வே", url: "https://www.subway.com/", keywords: ["Subway", "Sandwiches", "Fast Food", "Healthy"] },
            { name: "டொமினோஸ்", url: "https://www.dominos.com/", keywords: ["Dominos", "Pizza", "Delivery", "Food"] },
            { name: "பிஸ்ஸா ஹட்", url: "https://www.pizzahut.com/", keywords: ["Pizza Hut", "Pizza", "Delivery", "Food"] },
            { name: "சிக்கன் ஃபில் ஏ", url: "https://www.chick-fil-a.com/", keywords: ["Chick-fil-A", "Chicken", "Sandwiches", "Fast Food"] },
            { name: "பர்கர் கிங்", url: "https://www.bk.com/", keywords: ["Burger King", "Burgers", "Fast Food", "Fries"] },
            { name: "வெண்டிஸ்", url: "https://www.wendys.com/", keywords: ["Wendy's", "Burgers", "Fast Food", "Salads"] },
            { name: "டன்கின் டோனட்ஸ்", url: "https://www.dunkindonuts.com/", keywords: ["Dunkin' Donuts", "Coffee", "Donuts", "Breakfast"] },
            { name: "பாபா ஜான்ஸ்", url: "https://www.papajohns.com/", keywords: ["Papa John's", "Pizza", "Delivery", "Food"] },
            { name: "உபெர்", url: "https://www.uber.com/", keywords: ["Uber", "Ride Sharing", "Transportation", "Taxi"] },
            { name: "லிஃப்ட்", url: "https://www.lyft.com/", keywords: ["Lyft", "Ride Sharing", "Transportation", "Taxi"] },
            { name: "ஏர்பின்பி", url: "https://www.airbnb.com/", keywords: ["Airbnb", "Travel", "Vacation Rentals", "Lodging"] },
            { name: "Booking.com", url: "https://www.booking.com/", keywords: ["Booking.com", "Hotels", "Travel", "Reservations"] },
            { name: "Expedia", url: "https://www.expedia.com/", keywords: ["Expedia", "Travel", "Flights", "Hotels"] },
            { name: "Kayak", url: "https://www.kayak.com/", keywords: ["Kayak", "Travel", "Flights", "Hotels"] },
            { name: "Priceline", url: "https://www.priceline.com/", keywords: ["Priceline", "Travel", "Deals", "Hotels"] },
            { name: "TripAdvisor", url: "https://www.tripadvisor.com/", keywords: ["TripAdvisor", "Travel", "Reviews", "Hotels"] },
            { name: "ஹோட்டல்ஸ்.காம்", url: "https://www.hotels.com/", keywords: ["Hotels.com", "Hotels", "Reservations", "Travel"] },
            { name: "Vrbo", url: "https://www.vrbo.com/", keywords: ["Vrbo", "Vacation Rentals", "Travel", "Lodging"] },
            { name: "ஸோஹோ", url: "https://www.zoho.com/", keywords: ["Zoho", "CRM", "Business", "Software"] },
            { name: "Salesforce", url: "https://www.salesforce.com/", keywords: ["Salesforce", "CRM", "Sales", "Business"] },
            { name: "HubSpot", url: "https://www.hubspot.com/", keywords: ["HubSpot", "Marketing", "CRM", "Sales"] },
            { name: "Oracle", url: "https://www.oracle.com/", keywords: ["Oracle", "Database", "Software", "Enterprise"] },
            { name: "SAP", url: "https://www.sap.com/", keywords: ["SAP", "Enterprise", "Software", "Business"] },
            { name: "Workday", url: "https://www.workday.com/", keywords: ["Workday", "HR", "Finance", "Software"] },
            { name: "ServiceNow", url: "https://www.servicenow.com/", keywords: ["ServiceNow", "IT Management", "Software", "Enterprise"] },
            { name: "Intuit", url: "https://www.intuit.com/", keywords: ["Intuit", "QuickBooks", "TurboTax", "Finance"] },
            { name: "Xero", url: "https://www.xero.com/", keywords: ["Xero", "Accounting", "Small Business", "Finance"] },
            { name: "Square", url: "https://squareup.com/", keywords: ["Square", "Payments", "POS", "Small Business"] },
            { name: "Canva", url: "https://www.canva.com/", keywords: ["Canva", "Design", "Graphics", "Templates"] },
            { name: "Figma", url: "https://www.figma.com/", keywords: ["Figma", "Design", "Collaboration", "UI"] },
            { name: "Sketch", url: "https://www.sketch.com/", keywords: ["Sketch", "Design", "UI", "Mac"] },
            { name: "Adobe XD", url: "https://www.adobe.com/products/xd.html", keywords: ["Adobe XD", "Design", "UI", "Prototyping"] },
            { name: "CorelDRAW", url: "https://www.coreldraw.com/", keywords: ["CorelDRAW", "Design", "Graphics", "Vector"] },
            { name: "ஜிம்ப்", url: "https://www.gimp.org/", keywords: ["GIMP", "Image Editing", "Free", "Open Source"] },
            { name: "Inkscape", url: "https://inkscape.org/", keywords: ["Inkscape", "Vector Graphics", "Free", "Open Source"] },
            { name: "Blender", url: "https://www.blender.org/", keywords: ["Blender", "3D", "Modeling", "Animation"] },
            { name: "AutoCAD", url: "https://www.autodesk.com/products/autocad/", keywords: ["AutoCAD", "CAD", "Design", "Engineering"] },
            { name: "SolidWorks", url: "https://www.solidworks.com/", keywords: ["SolidWorks", "3D CAD", "Engineering", "Design"] },
            { name: "Unity", url: "https://unity.com/", keywords: ["Unity", "Game Development", "3D", "Engine"] },
            { name: "Unreal Engine", url: "https://www.unrealengine.com/", keywords: ["Unreal Engine", "Game Development", "3D", "Engine"] },
            { name: "Maya", url: "https://www.autodesk.com/products/maya/", keywords: ["Maya", "3D", "Animation", "Modeling"] },
            { name: "3ds Max", url: "https://www.autodesk.com/products/3ds-max/", keywords: ["3ds Max", "3D", "Modeling", "Animation"] },
            { name: "Final Cut Pro", url: "https://www.apple.com/final-cut-pro/", keywords: ["Final Cut Pro", "Video Editing", "Apple", "Software"] },
            { name: "Adobe Premiere Pro", url: "https://www.adobe.com/products/premiere.html", keywords: ["Adobe Premiere Pro", "Video Editing", "Professional", "Software"] },
            { name: "Avid Media Composer", url: "https://www.avid.com/products/media-composer", keywords: ["Avid Media Composer", "Video Editing", "Film", "Television"] },
            { name: "DaVinci Resolve", url: "https://www.blackmagicdesign.com/products/davinciresolve/", keywords: ["DaVinci Resolve", "Video Editing", "Color Grading", "Post Production"] },
            { name: "iMovie", url: "https://www.apple.com/imovie/", keywords: ["iMovie", "Video Editing", "Apple", "Home"] },
            { name: "Audacity", url: "https://www.audacityteam.org/", keywords: ["Audacity", "Audio Editing", "Free", "Open Source"] },
            { name: "Ableton Live", url: "https://www.ableton.com/", keywords: ["Ableton Live", "Music Production", "DAW", "Audio"] },
            { name: "FL Studio", url: "https://www.image-line.com/", keywords: ["FL Studio", "Music Production", "DAW", "Beatmaking"] },
            { name: "Logic Pro", url: "https://www.apple.com/logic-pro/", keywords: ["Logic Pro", "Music Production", "DAW", "Apple"] },
             { name: "Pro Tools", url: "https://www.avid.com/products/pro-tools", keywords: ["Pro Tools", "Audio", "Recording", "Mixing"] },
            { name: "Python", url: "https://www.python.org/", keywords: ["Python", "Programming", "Language", "Coding"] },
            { name: "Java", url: "https://www.java.com/", keywords: ["Java", "Programming", "Language", "Software"] },
            { name: "JavaScript", url: "https://www.javascript.com/", keywords: ["JavaScript", "Programming", "Web Development", "Frontend"] },
            { name: "C++", url: "https://isocpp.org/", keywords: ["C++", "Programming", "Language", "Systems"] },
            { name: "C#", url: "https://dotnet.microsoft.com/en-us/languages/csharp", keywords: ["C#", "Programming", "Microsoft", "Game Development"] },
            { name: "Ruby", url: "https://www.ruby-lang.org/", keywords: ["Ruby", "Programming", "Web Development", "Rails"] },
            { name: "PHP", url: "https://www.php.net/", keywords: ["PHP", "Programming", "Web Development", "Server Side"] },
            { name: "Swift", url: "https://developer.apple.com/swift/", keywords: ["Swift", "Programming", "Apple", "iOS Development"] },
            { name: "Kotlin", url: "https://kotlinlang.org/", keywords: ["Kotlin", "Programming", "Android Development", "Google"] },
            { name: "Go", url: "https://go.dev/", keywords: ["Go", "Programming", "Google", "Systems"] },
            { name: "Rust", url: "https://www.rust-lang.org/", keywords: ["Rust", "Programming", "Systems", "Memory Safety"] },
            { name: "TypeScript", url: "https://www.typescriptlang.org/", keywords: ["TypeScript", "Programming", "JavaScript", "Frontend"] },
            { name: "SQL", url: "https://www.iso.org/standard/63555.html", keywords: ["SQL", "Database", "Querying", "Data"] },
            { name: "Perl", url: "https://www.perl.org/", keywords: ["Perl", "Programming", "Scripting", "System Administration"] },
            { name: "R", url: "https://www.r-project.org/", keywords: ["R", "Statistics", "Data Analysis", "Programming"] },
            { name: "Matlab", url: "https://www.mathworks.com/products/matlab.html", keywords: ["Matlab", "Mathematics", "Engineering", "Programming"] },
            { name: "Assembly", url: "https://www.assemblylanguage.com/", keywords: ["Assembly", "Programming", "Low-Level", "Hardware"] },
            { name: "Scala", url: "https://www.scala-lang.org/", keywords: ["Scala", "Programming", "JVM", "Functional"] },
            { name: "Haskell", url: "https://www.haskell.org/", keywords: ["Haskell", "Programming", "Functional", "Purity"] },
            { name: "Julia", url: "https://julialang.org/", keywords: ["Julia", "Programming", "Scientific Computing", "High-Performance"] },
            { name: "Dart", url: "https://dart.dev/", keywords: ["Dart", "Programming", "Flutter", "Mobile Development"] },
            { name: "PHPMyAdmin", url: "https://www.phpmyadmin.net/", keywords: ["PHPMyAdmin", "Database", "MySQL", "Admin"] },
            { name: "Apache", url: "https://httpd.apache.org/", keywords: ["Apache", "Web Server", "Server", "HTTP"] },
            { name: "Nginx", url: "https://www.nginx.com/", keywords: ["Nginx", "Web Server", "Reverse Proxy", "Load Balancing"] },
            { name: "Docker", url: "https://www.docker.com/", keywords: ["Docker", "Containers", "DevOps", "Deployment"] },
            { name: "Kubernetes", url: "https://kubernetes.io/", keywords: ["Kubernetes", "Containers", "Orchestration", "Cloud"] },
            { name: "AWS", url: "https://aws.amazon.com/", keywords: ["AWS", "Cloud", "Amazon Web Services", "Computing"] },
            { name: "Azure", url: "https://azure.microsoft.com/", keywords: ["Azure", "Cloud", "Microsoft", "Computing"] },
            { name: "Google Cloud", url: "https://cloud.google.com/", keywords: ["Google Cloud", "Cloud", "GCP", "Computing"] },
            { name: "Heroku", url: "https://www.heroku.com/", keywords: ["Heroku", "Cloud", "Platform as a Service", "PaaS"] },
            { name: "DigitalOcean", url: "https://www.digitalocean.com/", keywords: ["DigitalOcean", "Cloud", "VPS", "Developers"] },
            { name: "Linode", url: "https://www.linode.com/", keywords: ["Linode", "Cloud", "VPS", "Servers"] },
            { name: "Vercel", url: "https://vercel.com/", keywords: ["Vercel", "Frontend", "Deployment", "Next.js"] },
            { name: "Netlify", url: "https://www.netlify.com/", keywords: ["Netlify", "Frontend", "Deployment", "Jamstack"] },
            { name: "Cloudflare", url: "https://www.cloudflare.com/", keywords: ["Cloudflare", "CDN", "Security", "DNS"] },
            { name: "Akamai", url: "https://www.akamai.com/", keywords: ["Akamai", "CDN", "Security", "Performance"] },
            { name: "Fastly", url: "https://www.fastly.com/", keywords: ["Fastly", "CDN", "Cloud", "Edge"] },
            { name: "Firebase", url: "https://firebase.google.com/", keywords: ["Firebase", "Backend", "Mobile", "Google"] },
            { name: "MongoDB", url: "https://www.mongodb.com/", keywords: ["MongoDB", "Database", "NoSQL", "Document"] },
            { name: "PostgreSQL", url: "https://www.postgresql.org/", keywords: ["PostgreSQL", "Database", "SQL", "Open Source"] },
            { name: "MySQL", url: "https://www.mysql.com/", keywords: ["MySQL", "Database", "SQL", "Open Source"] },
            { name: "Redis", url: "https://redis.io/", keywords: ["Redis", "Cache", "Database", "NoSQL"] },
            { name: "Elasticsearch", url: "https://www.elastic.co/", keywords: ["Elasticsearch", "Search", "Analytics", "Data"] },
            { name: "Kafka", url: "https://kafka.apache.org/", keywords: ["Kafka", "Streaming", "Data", "Messaging"] },
            { name: "RabbitMQ", url: "https://www.rabbitmq.com/", keywords: ["RabbitMQ", "Messaging", "Queue", "Broker"] },
            { name: "Jenkins", url: "https://www.jenkins.io/", keywords: ["Jenkins", "CI/CD", "Automation", "DevOps"] },
            { name: "GitLab", url: "https://about.gitlab.com/", keywords: ["GitLab", "DevOps", "Repository", "CI/CD"] },
            { name: "Travis CI", url: "https://www.travis-ci.com/", keywords: ["Travis CI", "CI/CD", "Testing", "Automation"] },
            { name: "CircleCI", url: "https://circleci.com/", keywords: ["CircleCI", "CI/CD", "Automation", "DevOps"] },
            { name: "Jira", url: "https://www.atlassian.com/software/jira", keywords: ["Jira", "Project Management", "Agile", "Tickets"] },
            { name: "Confluence", url: "https://www.atlassian.com/software/confluence", keywords: ["Confluence", "Collaboration", "Documentation", "Wiki"] },
            { name: "Bitbucket", url: "https://bitbucket.org/", keywords: ["Bitbucket", "Repository", "Git", "Code"] },
            { name: "SVN", url: "https://subversion.apache.org/", keywords: ["SVN", "Version Control", "Repository", "Code"] },
            { name: "Selenium", url: "https://www.selenium.dev/", keywords: ["Selenium", "Testing", "Automation", "Web"] },
            { name: "JUnit", url: "https://junit.org/", keywords: ["JUnit", "Testing", "Java", "Unit"] },
            { name: "TestNG", url: "https://testng.org/", keywords: ["TestNG", "Testing", "Java", "Framework"] },
            { name: "Mockito", url: "https://site.mockito.org/", keywords: ["Mockito", "Testing", "Java", "Mocking"] },
            { name: "Spring", url: "https://spring.io/", keywords: ["Spring", "Java", "Framework", "Development"] },
            { name: "Django", url: "https://www.djangoproject.com/", keywords: ["Django", "Python", "Framework", "Web Development"] },
            { name: "Flask", url: "https://flask.palletsprojects.com/", keywords: ["Flask", "Python", "Framework", "Web Development"] },
            { name: "Ruby on Rails", url: "https://rubyonrails.org/", keywords: ["Ruby on Rails", "Ruby", "Framework", "Web Development"] },
            { name: "Laravel", url: "https://laravel.com/", keywords: ["Laravel", "PHP", "Framework", "Web Development"] },
            { name: "ASP.NET", url: "https://dotnet.microsoft.com/en-us/apps/aspnet", keywords: ["ASP.NET", "C#", "Microsoft", "Web Development"] },
            { name: "Node.js", url: "https://nodejs.org/", keywords: ["Node.js", "JavaScript", "Server-side", "Runtime"] },
            { name: "React", url: "https://react.dev/", keywords: ["React", "JavaScript", "Frontend", "UI"] },
            { name: "Angular", url: "https://angular.io/", keywords: ["Angular", "JavaScript", "Frontend", "Framework"] },
            { name: "Vue.js", url: "https://vuejs.org/", keywords: ["Vue.js", "JavaScript", "Frontend", "UI"] },
            { name: "jQuery", url: "https://jquery.com/", keywords: ["jQuery", "JavaScript", "Library", "DOM"] },
            { name: "Bootstrap", url: "https://getbootstrap.com/", keywords: ["Bootstrap", "CSS", "Framework", "UI"] },
            { name: "Tailwind CSS", url: "https://tailwindcss.com/", keywords: ["Tailwind CSS", "CSS", "Framework", "Styling"] },
            { name: "Sass", url: "https://sass-lang.com/", keywords: ["Sass", "CSS", "Preprocessor", "Styles"] },
            { name: "Less", url: "http://lesscss.org/", keywords: ["Less", "CSS", "Preprocessor", "Styles"] },
            { name: "Material UI", url: "https://mui.com/", keywords: ["Material UI", "React", "UI", "Components"] },
            { name: "Ant Design", url: "https://ant.design/", keywords: ["Ant Design", "React", "UI", "Components"] },
            { name: "Chakra UI", url: "https://chakra-ui.com/", keywords: ["Chakra UI", "React", "UI", "Components"] },
            { name: "Redux", url: "https://redux.js.org/", keywords: ["Redux", "State Management", "JavaScript", "React"] },
            { name: "GraphQL", url: "https://graphql.org/", keywords: ["GraphQL", "API", "Query Language", "Data"] },
            { name: "REST", url: "https://restfulapi.net/", keywords: ["REST", "API", "Web Services", "HTTP"] },
            { name: "Swagger", url: "https://swagger.io/", keywords: ["Swagger", "API", "Documentation", "Tools"] },
            { name: "Postman", url: "https://www.postman.com/", keywords: ["Postman", "API", "Testing", "Development"] },
            { name: "Insomnia", url: "https://insomnia.rest/", keywords: ["Insomnia", "API", "Testing", "Client"] },
            { name: "WebSockets", url: "https://www.websocket.org/", keywords: ["WebSockets", "Real-time", "Communication", "Protocol"] },
            { name: "Socket.IO", url: "https://socket.io/", keywords: ["Socket.IO", "Real-time", "Communication", "Library"] },
            { name: "WebRTC", url: "https://webrtc.org/", keywords: ["WebRTC", "Real-time", "Communication", "Video"] },
            { name: "Zoom", url: "https://zoom.us/", keywords: ["Zoom", "Video Conferencing", "Meetings", "Communication"] },
            { name: "Microsoft Teams", url: "https://www.microsoft.com/en-in/microsoft-teams/group-chat-software", keywords: ["Microsoft Teams", "Collaboration", "Chat", "Meetings"] },
            { name: "Slack", url: "https://slack.com/", keywords: ["Slack", "Communication", "Team", "Chat"] },
            { name: "Discord", url: "https://discord.com/", keywords: ["Discord", "Communication", "Community", "Chat"] },
            { name: "Twilio", url: "https://www.twilio.com/", keywords: ["Twilio", "Communication", "API", "SMS"] },
            { name: "SendGrid", url: "https://sendgrid.com/", keywords: ["SendGrid", "Email", "API", "Delivery"] },
            { name: "Mailchimp", url: "https://mailchimp.com/", keywords: ["Mailchimp", "Email Marketing", "Campaigns", "Newsletter"] },
            { name: "Constant Contact", url: "https://www.constantcontact.com/", keywords: ["Constant Contact", "Email Marketing", "Tools", "Business"] },
            { name: "AWeber", url: "https://www.aweber.com/", keywords: ["AWeber", "Email Marketing", "Automation", "List"] },
            { name: "Stripe", url: "https://stripe.com/", keywords: ["Stripe", "Payments", "Online", "Transactions"] },
            { name: "PayPal", url: "https://www.paypal.com/", keywords: ["PayPal", "Payments", "Online", "Money"] },
            { name: "Square", url: "https://squareup.com/", keywords: ["Square", "Payments", "POS", "Business"] },
            { name: "Braintree", url: "https://www.braintreepayments.com/", keywords: ["Braintree", "Payments", "PayPal", "Developers"] },
            { name: "Authorize.Net", url: "https://www.authorize.net/", keywords: ["Authorize.Net", "Payments", "Visa", "Mastercard"] },
            { name: "Google Analytics", url: "https://analytics.google.com/", keywords: ["Google Analytics", "Analytics", "Tracking", "Data"] },
            { name: "Adobe Analytics", url: "https://www.adobe.com/analytics/adobe-analytics.html", keywords: ["Adobe Analytics", "Analytics", "Marketing", "Data"] },
            { name: "Mixpanel", url: "https://mixpanel.com/", keywords: ["Mixpanel", "Analytics", "Product", "Data"] },
            { name: "Kissmetrics", url: "https://www.kissmetrics.com/", keywords: ["Kissmetrics", "Analytics", "Behavioral", "Data"] },
            { name: "Matomo", url: "https://matomo.org/", keywords: ["Matomo", "Analytics", "Open Source", "Privacy"] },
            { name: "Hotjar", url: "https://www.hotjar.com/", keywords: ["Hotjar", "Analytics", "UX", "Behavior"] },
            { name: "Crazy Egg", url: "https://www.crazyegg.com/", keywords: ["Crazy Egg", "Analytics", "Heatmaps", "UX"] },
            { name: "Optimizely", url: "https://www.optimizely.com/", keywords: ["Optimizely", "Testing", "AB Testing", "Experimentation"] },
            { name: "VWO", url: "https://vwo.com/", keywords: ["VWO", "Testing", "AB Testing", "Optimization"] },
            { name: "Google Optimize", url: "https://optimize.google.com/", keywords: ["Google Optimize", "Testing", "AB Testing", "Personalization"] },
            { name: "SEMrush", url: "https://www.semrush.com/", keywords: ["SEMrush", "SEO", "Marketing", "Analytics"] },
            { name: "Ahrefs", url: "https://ahrefs.com/", keywords: ["Ahrefs", "SEO", "Tools", "Backlinks"] },
            { name: "Moz", url: "https://moz.com/", keywords: ["Moz", "SEO", "Software", "Tools"] },
            { name: "Yoast SEO", url: "https://yoast.com/", keywords: ["Yoast SEO", "WordPress", "Plugin", "SEO"] },
            { name: "Rank Math", url: "https://rankmath.com/", keywords: ["Rank Math", "WordPress", "Plugin", "SEO"] },
            { name: "Screaming Frog", url: "https://www.screamingfrog.co.uk/", keywords: ["Screaming Frog", "SEO", "Crawler", "Website"] },
            { name: "GTmetrix", url: "https://gtmetrix.com/", keywords: ["GTmetrix", "Performance", "Website", "Speed"] },
            { name: "PageSpeed Insights", url: "https://developers.google.com/speed/pagespeed/insights/", keywords: ["PageSpeed Insights", "Performance", "Website", "Google"] },
            { name: "WebPageTest", url: "https://www.webpagetest.org/", keywords: ["WebPageTest", "Performance", "Website", "Testing"] },
            { name: "Lighthouse", url: "https://developer.chrome.com/docs/lighthouse/", keywords: ["Lighthouse", "Performance", "Accessibility", "Chrome"] },
            { name: "New Relic", url: "https://newrelic.com/", keywords: ["New Relic", "Monitoring", "Performance", "APM"] },
            { name: "Datadog", url: "https://www.datadoghq.com/", keywords: ["Datadog", "Monitoring", "Metrics", "Logging"] },
            { name: "Splunk", url: "https://www.splunk.com/", keywords: ["Splunk", "Logging", "Security", "Data"] },
            { name: "ELK Stack", url: "https://www.elastic.co/elastic-stack/", keywords: ["ELK Stack", "Logging", "Search", "Analytics"] },
            { name: "Sentry", url: "https://sentry.io/", keywords: ["Sentry", "Error Tracking", "Monitoring", "Development"] },
            { name: "Raygun", url: "https://raygun.com/", keywords: ["Raygun", "Error Tracking", "Performance", "Monitoring"] },
            { name: "LogRocket", url: "https://logrocket.com/", keywords: ["LogRocket", "Session Replay", "Monitoring", "Frontend"] },
            { name: "FullStory", url: "https://www.fullstory.com/", keywords: ["FullStory", "Session Replay", "Analytics", "UX"] },
            { name: "Heap", url: "https://heap.io/", keywords: ["Heap", "Analytics", "Product", "Data"] },
            { name: "Amplitude", url: "https://amplitude.com/", keywords: ["Amplitude", "Analytics", "Mobile", "Product"] },
            { name: "Pendo", url: "https://www.pendo.io/", keywords: ["Pendo", "Product Experience", "Analytics", "Engagement"] },
            { name: "Intercom", url: "https://www.intercom.com/", keywords: ["Intercom", "Customer Communication", "Chat", "Support"] },
            { name: "Zendesk", url: "https://www.zendesk.com/", keywords: ["Zendesk", "Customer Service", "Support", "Tickets"] },
            { name: "Salesforce Service Cloud", url: "https://www.salesforce.com/in/service-cloud/", keywords: ["Salesforce Service Cloud", "CRM", "Customer Service", "Support"] },
            { name: "Freshdesk", url: "https://www.freshworks.com/freshdesk/", keywords: ["Freshdesk", "Customer Service", "Support", "Helpdesk"] },
            { name: "HubSpot Service Hub", url: "https://www.hubspot.com/products/service", keywords: ["HubSpot Service Hub", "Customer Service", "Support", "CRM"] },
            { name: "LiveChat", url: "https://www.livechat.com/", keywords: ["LiveChat", "Customer Service", "Chat", "Support"] },
            { name: "Tawk.to", url: "https://www.tawk.to/", keywords: ["Tawk.to", "Customer Service", "Chat", "Free"] },
            { name: "Crisp", url: "https://crisp.chat/", keywords: ["Crisp", "Customer Service", "Chat", "Marketing"] },
            { name: "Olark", url: "https://www.olark.com/", keywords: ["Olark", "Customer Service", "Chat", "Sales"] },
            { name: "SnapEngage", url: "https://snapengage.com/", keywords: ["SnapEngage", "Customer Service", "Chat", "Proactive"] },
            { name: "WhatsApp", url: "https://www.whatsapp.com/", keywords: ["WhatsApp", "Messaging", "Chat", "Social"] },
            { name: "Facebook Messenger", url: "https://www.messenger.com/", keywords: ["Facebook Messenger", "Messaging", "Chat", "Social"] },
            { name: "WeChat", url: "https://www.wechat.com/", keywords: ["WeChat", "Messaging", "Social", "China"] },
            { name: "Telegram", url: "https://telegram.org/", keywords: ["Telegram", "Messaging", "Chat", "Secure"] },
            { name: "Signal", url: "https://signal.org/", keywords: ["Signal", "Messaging", "Privacy", "Secure"] },
            { name: "Line", url: "https://line.me/en/", keywords: ["Line", "Messaging", "Social", "Asia"] },
            { name: "Viber", url: "https://www.viber.com/", keywords: ["Viber", "Messaging", "Call", "International"] },
            { name: "KakaoTalk", url: "https://kakao.com/", keywords: ["KakaoTalk", "Messaging", "Social", "Korea"] },
            { name: "Skype", url: "https://www.skype.com/", keywords: ["Skype", "Video Call", "Chat", "Communication"] },
            { name: "FaceTime", url: "https://www.apple.com/facetime/", keywords: ["FaceTime", "Video Call", "Apple", "Communication"] },
            { name: "LinkedIn Learning", url: "https://www.linkedin.com/learning/", keywords: ["LinkedIn Learning", "Education", "Courses", "Professional"] },
            { name: "Coursera", url: "https://www.coursera.org/", keywords: ["Coursera", "Education", "Courses", "Online"] },
            { name: "edX", url: "https://www.edx.org/", keywords: ["edX", "Education", "Courses", "University"] },
            { name: "Udacity", url: "https://www.udacity.com/", keywords: ["Udacity", "Education", "Nanodegree", "Tech"] },
            { name: "Udemy", url: "https://www.udemy.com/", keywords: ["Udemy", "Education", "Courses", "Online"] },
            { name: "Khan Academy", url: "https://www.khanacademy.org/", keywords: ["Khan Academy", "Education", "Free", "Learning"] },
            { name: "Skillshare", url: "https://www.skillshare.com/", keywords: ["Skillshare", "Education", "Creative", "Classes"] },
            { name: "MasterClass", url: "https://www.masterclass.com/", keywords: ["MasterClass", "Education", "Celebrity", "Classes"] },
            { name: "Teachable", url: "https://teachable.com/", keywords: ["Teachable", "Education", "Online Courses", "Platform"] },
            { name: "Thinkific", url: "https://www.thinkific.com/", keywords: ["Thinkific", "Education", "Online Courses", "Platform"] },
            { name: "WordPress.org", url: "https://wordpress.org/", keywords: ["WordPress", "CMS", "Blog", "Website"] },
            { name: "Joomla", url: "https://www.joomla.org/", keywords: ["Joomla", "CMS", "Website", "Open Source"] },
            { name: "Drupal", url: "https://www.drupal.org/", keywords: ["Drupal", "CMS", "Website", "Development"] },
            { name: "Wix", url: "https://www.wix.com/", keywords: ["Wix", "Website Builder", "Drag and Drop", "Hosting"] },
            { name: "Squarespace", url: "https://www.squarespace.com/", keywords: ["Squarespace", "Website Builder", "Design", "E-commerce"] },
            { name: "Shopify", url: "https://www.shopify.com/", keywords: ["Shopify", "E-commerce", "Online Store", "Business"] },
            { name: "BigCommerce", url: "https://www.bigcommerce.com/", keywords: ["BigCommerce", "E-commerce", "Online Store", "Platform"] },
            { name: "Magento", url: "https://magento.com/", keywords: ["Magento", "E-commerce", "Open Source", "Adobe"] },
            { name: "WooCommerce", url: "https://woocommerce.com/", keywords: ["WooCommerce", "E-commerce", "WordPress", "Plugin"] },
            { name: "PrestaShop", url: "https://www.prestashop.com/", keywords: ["PrestaShop", "E-commerce", "Open Source", "Platform"] },
            { name: "ZoomInfo", url: "https://www.zoominfo.com/", keywords: ["ZoomInfo", "Business", "Information", "Sales"] },
            { name: "Crunchbase", url: "https://www.crunchbase.com/", keywords: ["Crunchbase", "Startups", "Investors", "Business"] },
            { name: "Owler", url: "https://www.owler.com/", keywords: ["Owler", "Business", "Intelligence", "Competition"] },
            { name: "D&B Hoovers", url: "https://www.dnb.com/business-directory/hoovers.html", keywords: ["D&B Hoovers", "Business", "Data", "Sales"] },
            { name: "SimilarWeb", url: "https://www.similarweb.com/", keywords: ["SimilarWeb", "Website", "Analytics", "Competition"] },
            { name: "Built With", url: "https://builtwith.com/", keywords: ["Built With", "Technology", "Websites", "Tools"] },
            { name: "SpyFu", url: "https://www.spyfu.com/", keywords: ["SpyFu", "SEO", "Keywords", "Competition"] },
            { name: "Alexa", url: "https://www.alexa.com/", keywords: ["Alexa", "Website Ranking", "SEO", "Amazon"] },
             { name: "SEMrush", url: "https://www.semrush.com/", keywords: ["SEMrush", "SEO", "Marketing", "Research"] },
            { name: "Glassdoor", url: "https://www.glassdoor.com/", keywords: ["Glassdoor", "Jobs", "Reviews", "Salaries"] },
            { name: "Indeed", url: "https://www.indeed.com/", keywords: ["Indeed", "Jobs", "Search", "Careers"] },
            { name: "LinkedIn", url: "https://www.linkedin.com/", keywords: ["LinkedIn", "Jobs", "Networking", "Professional"] },
            { name: "Monster", url: "https://www.monster.com/", keywords: ["Monster", "Jobs", "Search", "Careers"] },
            { name: "CareerBuilder", url: "https://www.careerbuilder.com/", keywords: ["CareerBuilder", "Jobs", "Search", "Careers"] },
            { name: "ZipRecruiter", url: "https://www.ziprecruiter.com/", keywords: ["ZipRecruiter", "Jobs", "Search", "Hiring"] },
            { name: "SimplyHired", url: "https://www.simplyhired.com/", keywords: ["SimplyHired", "Jobs", "Search", "Careers"] },
            { name: "Google Jobs", url: "https://www.google.com/search?q=google+jobs", keywords: ["Google Jobs", "Jobs", "Search", "Careers"] },
            { name: "AngelList", url: "https://angel.co/", keywords: ["AngelList", "Startups", "Jobs", "Investors"] },
            { name: "Dice", url: "https://www.dice.com/", keywords: ["Dice", "Tech Jobs", "Careers", "Developers"] },
            { name: "Zillow", url: "https://www.zillow.com/", keywords: ["Zillow", "Real Estate", "Homes For Sale", "Rentals"] },
            { name: "Redfin", url: "https://www.redfin.com/", keywords: ["Redfin", "Real Estate", "Homes For Sale", "Agents"] },
            { name: "Realtor.com", url: "https://www.realtor.com/", keywords: ["Realtor.com", "Real Estate", "Homes For Sale", "Find an Agent"] },
            { name: "Trulia", url: "https://www.trulia.com/", keywords: ["Trulia", "Real Estate", "Homes For Sale", "Neighborhoods"] },
            { name: "Apartments.com", url: "https://www.apartments.com/", keywords: ["Apartments.com", "Apartments", "Rentals", "Housing"] },
            { name: "Rent.com", url: "https://www.rent.com/", keywords: ["Rent.com", "Apartments", "Rentals", "Housing"] },
            { name: "Zumper", url: "https://www.zumper.com/", keywords: ["Zumper", "Apartments", "Rentals", "Housing"] },
            { name: "HotPads", url: "https://hotpads.com/", keywords: ["HotPads", "Apartments", "Rentals", "Housing"] },
             { name: "LoopNet", url: "https://www.loopnet.com/", keywords: ["LoopNet", "Commercial Real Estate", "For Sale", "Lease"] },
            { name: "CoStar", url: "https://www.costar.com/", keywords: ["CoStar", "Commercial Real Estate", "Data", "Analytics"] },

   ];

  function searchWebsites(query) {
            const resultsContainer = document.getElementById("resultsContainer");
            resultsContainer.innerHTML = ""; // Clear previous results
    if (!query) {
                resultsContainer.innerHTML = "<p class='text-gray-500 text-center'>Please enter a search query.</p>";
                return;
            }
    const matchingWebsites = websiteData.filter(website => {
                const queryLower = query.toLowerCase();
                return (
                    website.name.toLowerCase().includes(queryLower) ||
                    website.keywords.some(keyword => keyword.toLowerCase().includes(queryLower))
                );
            });

  if (matchingWebsites.length === 0) {
                resultsContainer.innerHTML = "<p class='text-gray-500 text-center'>No matching websites found.</p>";
            } else {
                const resultsHTML = matchingWebsites.map(website => `
  <div class="bg-white rounded-lg shadow-md p-4 mb-4">
                        <h2 class="text-lg font-semibold text-blue-600 hover:underline">
                            <a href="${website.url}" target="_blank">${website.name}</a>
                        </h2>
                        <p class="text-gray-700">${website.url}</p>
                    </div>
                `).join("");
                resultsContainer.innerHTML = resultsHTML;
            }
        }

  document.getElementById("searchButton").addEventListener("click", () => {
            const query = document.getElementById("searchBar").value;
            searchWebsites(query);
        });

  document.getElementById("searchBar").addEventListener("keypress", (event) => {
            if (event.key === "Enter") {
                const query = document.getElementById("searchBar").value;
                searchWebsites(query);
            }
           // Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyChRXmoyYliaaHNzv52CC-PAj6VT7OP-do",
  authDomain: "drfebh5n.firebaseapp.com",
  projectId: "drfebh5n",
  storageBucket: "drfebh5n.firebasestorage.app",
  messagingSenderId: "829151375812",
  appId: "1:829151375812:web:0f354dbbfee4211b2ab491"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
"site": "undefined",
        });
    </script>
</body>
</html>
