<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PUBALI BANK TERMINAL MANAGEMENT</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom styles for Inter font and general body styling */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f2f5; /* Light gray background */
            color: #333;
            line-height: 1.6;
            text-transform: uppercase; /* Apply uppercase to all text in the body */
        }
        /* Basic styling for sections */
        .card {
            background-color: #fff;
            border-radius: 0.75rem; /* Rounded corners */
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* Subtle shadow */
            padding: 1.5rem;
            margin-bottom: 1.5rem;
        }
        /* Style for buttons */
        .btn {
            display: inline-block;
            padding: 0.75rem 1.5rem;
            border-radius: 0.5rem;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s ease-in-out, transform 0.1s ease-in-out;
        }
        .btn-primary {
            background-color: #4f46e5; /* Indigo */
            color: #fff;
        }
        .btn-primary:hover {
            background-color: #4338ca; /* Darker indigo */
            transform: translateY(-1px);
        }
        .btn-secondary {
            background-color: #6b7280; /* Gray */
            color: #fff;
        }
        .btn-secondary:hover {
            background-color: #4b5563; /* Darker gray */
            transform: translateY(-1px);
        }
        .btn-transfer {
            background-color: #f59e0b; /* Amber */
            color: #fff;
            padding: 0.4rem 0.8rem; /* Smaller padding for action button */
            font-size: 0.75rem; /* Smaller font for action button */
        }
        .btn-transfer:hover {
            background-color: #d97706; /* Darker Amber */
            transform: translateY(-1px);
        }

        /* Table styling */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 1rem;
        }
        th, td {
            padding: 0.5rem; /* Reduced padding for smaller cells */
            text-align: left;
            border-bottom: 1px solid #e5e7eb; /* Light gray border */
            font-size: 0.75rem; /* Even smaller text size (12px) */
            /* Default for all cells: no wrap, ellipsis */
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        th {
            background-color: #f9fafb; /* Lighter gray for header */
            font-weight: 600;
            color: #4b5563;
        }
        tr:hover {
            background-color: #f3f4f6; /* Hover effect for rows */
        }
        textarea, input, select {
            text-transform: none; /* Input fields should not force uppercase on user input */
        }
        /* Style for file input label to make it look like a button */
        .file-upload-label {
            display: inline-block;
            padding: 0.75rem 1.5rem;
            border-radius: 0.5rem;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s ease-in-out, transform 0.1s ease-in-out;
            background-color: #10b981; /* Emerald Green */
            color: #fff;
            text-align: center;
        }
        .file-upload-label:hover {
            background-color: #059669; /* Darker Emerald Green */
            transform: translateY(-1px);
        }
        .file-input {
            display: none; /* Hide the actual file input */
        }

        /* Custom styles for the compact search bar and download button */
        .controls-row-container {
            display: flex; /* Always visible and flex */
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 0.75rem; /* Reduced margin */
            flex-grow: 1; /* Allow it to take available space */
            justify-content: flex-end; /* Push content to the right */
        }
        .compact-search-input {
            flex-grow: 1; /* Allow search input to grow */
            max-width: 200px; /* Limit search input width */
            padding: 0.375rem 0.75rem; /* Smaller padding */
            font-size: 0.875rem; /* Smaller font size */
            border: 1px solid #d1d5db;
            border-radius: 0.375rem; /* Slightly less rounded */
            box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
            transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
        }
        .compact-search-input:focus {
            outline: none;
            border-color: #6366f1; /* Indigo-500 */
            box-shadow: 0 0 0 2px rgba(99, 102, 241, 0.25); /* Focus ring */
        }
        .compact-button {
            /* Calculate width based on icon size (1.125rem) + 2 * horizontal padding (0.625rem) */
            width: calc(1.125rem + 2 * 0.625rem); /* ~2.375rem */
            /* Calculate height based on icon size (1.125rem) + 2 * vertical padding (0.375rem) */
            height: calc(1.125rem + 2 * 0.375rem); /* ~1.875rem */
            padding: 0.375rem 0.625rem; /* Smaller padding for button */
            background-color: #4f46e5;
            color: #fff;
            border-radius: 0.375rem;
            box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
            transition: background-color 0.2s ease-in-out, transform 0.1s ease-in-out;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0; /* Prevent shrinking */
            flex-grow: 0; /* Prevent growing */
            line-height: 1; /* Ensure icon is centered */
        }
        .compact-button:hover {
            background-color: #4338ca;
            transform: translateY(-1px);
        }
        .compact-button svg {
            width: 1.125rem; /* Smaller icon size */
            height: 1.125rem;
        }

        /* Modal specific styles */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5); /* Semi-transparent black overlay */
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000; /* Ensure it's on top */
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s ease-in-out, visibility 0.3s ease-in-out;
        }
        .modal-overlay.show {
            opacity: 1;
            visibility: visible;
        }
        .modal-content {
            background-color: #fff;
            padding: 2rem;
            border-radius: 0.75rem;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
            width: 90%;
            max-width: 500px;
            position: relative;
            transform: translateY(-20px);
            transition: transform 0.3s ease-in-out;
        }
        .modal-overlay.show .modal-content {
            transform: translateY(0);
        }
        .modal-close-btn {
            position: absolute;
            top: 1rem;
            right: 1rem;
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #6b7280;
        }
        .modal-close-btn:hover {
            color: #333;
        }
        .modal-field {
            margin-bottom: 1rem;
        }
        .modal-field label {
            font-weight: 600;
            color: #4b5563;
            display: block;
            margin-bottom: 0.25rem;
        }
        .modal-field span {
            background-color: #f3f4f6;
            padding: 0.5rem 0.75rem;
            border-radius: 0.375rem;
            display: block;
            word-wrap: break-word; /* Allow long addresses to wrap */
            white-space: normal; /* Override nowrap from table cells */
        }

        /* Navbar specific styles */
        .navbar {
            background-color: #1a202c; /* Dark background for navbar */
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: #fff;
            border-radius: 0.75rem;
            margin-bottom: 1.5rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .navbar-brand {
            font-size: 1.5rem;
            font-weight: bold;
            color: #fff;
            text-decoration: none;
        }
        .dropdown {
            position: relative;
            display: inline-block;
        }
        .dropdown-button {
            background-color: #4f46e5;
            color: white;
            padding: 0.75rem 1.5rem;
            font-size: 1rem;
            border: none;
            cursor: pointer;
            border-radius: 0.5rem;
            transition: background-color 0.2s ease-in-out;
        }
        .dropdown-button:hover {
            background-color: #4338ca;
        }
        .dropdown-content {
            display: none; /* Hidden by default */
            position: absolute;
            background-color: #f9f9f9;
            min-width: 160px;
            box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
            z-index: 1;
            border-radius: 0.5rem;
            overflow: hidden;
            right: 0; /* Align dropdown to the right */
            margin-top: 0.5rem;
        }
        .dropdown-content.show-dropdown {
            display: block; /* Show when this class is present */
        }
        .dropdown-content a {
            color: black;
            padding: 12px 16px;
            text-decoration: none;
            display: block;
            text-align: left;
            transition: background-color 0.2s ease-in-out;
        }
        .dropdown-content a:hover {
            background-color: #ddd;
        }
        /* Removed .dropdown:hover .dropdown-content rule */
        .hidden-section {
            display: none;
        }

        /* Specific styles for the config generator section buttons */
        .config-generator-buttons button {
            background-color: #4f46e5; /* Indigo */
            color: #fff;
            padding: 0.5rem 1rem;
            border-radius: 0.375rem;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.2s ease-in-out;
            margin-right: 0.5rem; /* Space between buttons */
        }
        .config-generator-buttons button:hover {
            background-color: #4338ca; /* Darker indigo */
        }
        .config-generator-buttons button.action-button {
            background-color: #6b7280; /* Default grey for action buttons */
            color: #fff;
        }
        .config-generator-buttons button.action-button:hover {
            background-color: #4b5563;
        }
        .config-generator-buttons button.action-button[style*="background-color: rgb(255, 77, 3)"] {
            color: #000000; /* Black text for orange buttons */
        }
    </style>
</head>
<body class="p-4 sm:p-6 md:p-8">
    <div class="max-w-7xl mx-auto">
        <!-- Navbar -->
        <nav class="navbar">
            <a href="#" class="navbar-brand">PUBALI BANK</a>
            <div class="dropdown">
                <button class="dropdown-button" id="dropdownMenuButton">MENU</button>
                <div class="dropdown-content" id="myDropdown">
                    <a href="#" id="showDashboard">TERMINAL MANAGEMENT</a>
                    <!-- Removed: <a href="#" id="showConfigGenerator">CONFIGURATION GENERATOR</a> -->
                </div>
            </div>
        </nav>

        <!-- Main Heading (moved from body to specific section) -->
        <h1 class="text-4xl font-extrabold text-center text-gray-900 mb-8">PUBALI BANK TERMINAL MANAGEMENT</h1>

        <!-- Terminal Management Dashboard Section -->
        <div id="terminalDashboard" class="main-section">
            <!-- Terminal Overview Section -->
            <div class="card">
                <h2 class="text-2xl font-bold text-gray-800 mb-4">TERMINAL OVERVIEW</h2>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 text-center">
                    <div class="bg-blue-100 p-4 rounded-lg shadow-md">
                        <p class="text-lg font-semibold text-blue-800">TOTAL TERMINALS</p>
                        <p id="totalTerminals" class="text-4xl font-bold text-blue-600 mt-2">0</p>
                    </div>
                    <div class="bg-green-100 p-4 rounded-lg shadow-md">
                        <p class="text-lg font-semibold text-green-800">LIVE TERMINALS</p>
                        <p id="liveTerminals" class="text-4xl font-bold text-green-600 mt-2">0</p>
                    </div>
                    <div class="bg-red-100 p-4 rounded-lg shadow-md">
                        <p class="text-lg font-semibold text-red-800">WITHDRAWN TERMINALS</p>
                        <p id="withdrawnTerminals" class="text-4xl font-bold text-red-600 mt-2">0</p>
                    </div>
                </div>
            </div>

            <!-- App Version Breakdown Section -->
            <div class="card">
                <h2 class="text-2xl font-bold text-gray-800 mb-4">APP VERSION BREAKDOWN</h2>
                <div id="appVersionBreakdown" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                    <!-- App version cards will be inserted here by JavaScript -->
                </div>
            </div>

            <!-- Live Terminal Details Section -->
            <div class="card">
                <div class="flex justify-between items-center mb-4">
                    <h2 class="text-2xl font-bold text-gray-800">LIVE TERMINAL DETAILS</h2>
                    <div class="controls-row-container"> <!-- Combined container for search and download -->
                        <input type="text" id="liveSearchInput" class="compact-search-input" placeholder="SEARCH LIVE TERMINALS...">
                        <button id="liveSearchBtn" class="compact-button">
                            <!-- Search Icon (inline SVG) -->
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4">
                                <path fill-rule="evenodd" d="M10.5 3.75a6.75 6.75 0 1 0 0 13.5 6.75 6.75 0 0 0 0-13.5ZM2.25 10.5a8.25 8.25 0 1 1 14.59 5.28l4.69 4.69a.75.75 0 1 1-1.06 1.06l-4.69-4.69A8.25 8.25 0 0 1 2.25 10.5Z" clip-rule="evenodd" />
                            </svg>
                        </button>
                        <button id="liveDownloadBtn" class="compact-button bg-green-600 hover:bg-green-700">
                            <!-- Download Icon (inline SVG) -->
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4">
                                <path fill-rule="evenodd" d="M12 2.25a.75.75 0 0 1 .75.75v11.69l3.22-3.22a.75.75 0 1 1 1.06 1.06l-4.5 4.5a.75.75 0 0 1-1.06 0l-4.5-4.5a.75.75 0 1 1 1.06-1.06l3.22 3.22V3a.75.75 0 0 1 .75-.75ZM6.167 18.833a.75.75 0 0 1 1.08 0l2.5 2.5a.75.75 0 0 1-1.08 1.08l-2.5-2.5a.75.75 0 0 1 0-1.08ZM17.833 18.833a.75.75 0 0 1 0 1.08l-2.5 2.5a.75.75 0 0 1-1.08-1.08l2.5-2.5a.75.75 0 0 1 1.08 0Z" clip-rule="evenodd" />
                            </svg>
                        </button>
                    </div>
                </div>
                <div class="overflow-x-auto">
                    <table class="min-w-full bg-white rounded-lg shadow-md">
                        <thead>
                            <tr>
                                <th>S/N</th>
                                <th>TID</th>
                                <th>MID</th>
                                <th>MERCHANT NAME</th>
                                <th>DBA NAME</th>
                                <th>ADDRESS</th>
                                <th>BANK CONT. PERSON NAME</th>
                                <th>BANK CONT. PERSON NUMBER</th>
                                <th>DISTRICT</th>
                                <th>DIVISION</th>
                                <th>ZONE</th>
                                <th>POS S/N</th>
                                <th>POS BRAND & MODEL</th>
                                <th>OPERATOR NAME</th>
                                <th>SIM NUMBER</th>
                                <th>SIM IP</th>
                                <th>HOST IP</th>
                                <th>HOST PORT</th>
                                <th>VENDOR NAME</th>
                                <th>EMI</th>
                                <th>TENUR</th>
                                <th>REMARKS</th>
                                <th>CONFIGURE BY</th>
                                <th>CONFIGURE DATE</th>
                                <th>DEPLOY BY</th>
                                <th>DEPLOY DATE</th>
                                <th>ROLL-OUT BY</th>
                                <th>ROLL-OUT DATE</th>
                                <th>APP. VERSION</th>
                                <th>REMARKS-2</th>
                            </tr>
                        </thead>
                        <tbody id="liveTerminalListBody">
                            <!-- Live terminal rows will be inserted here by JavaScript -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Withdrawn Terminal Details Section -->
            <div class="card">
                <h2 class="text-2xl font-bold text-gray-800 mb-4">WITHDRAWN TERMINAL DETAILS</h2>
                <div class="overflow-x-auto">
                    <table class="min-w-full bg-white rounded-lg shadow-md">
                        <thead>
                            <tr>
                                <th>S/N</th>
                                <th>TID</th>
                                <th>MID</th>
                                <th>MERCHANT NAME</th>
                                <th>DBA NAME</th>
                                <th>ADDRESS</th>
                                <th>BANK CONT. PERSON NAME</th>
                                <th>BANK CONT. PERSON NUMBER</th>
                                <th>DISTRICT</th>
                                <th>DIVISION</th>
                                <th>ZONE</th>
                                <th>POS S/N</th>
                                <th>POS BRAND & MODEL</th>
                                <th>OPERATOR NAME</th>
                                <th>SIM NUMBER</th>
                                <th>SIM IP</th>
                                <th>HOST IP</th>
                                <th>HOST PORT</th>
                                <th>VENDOR NAME</th>
                                <th>EMI</th>
                                <th>TENUR</th>
                                <th>REMARKS</th>
                                <th>CONFIGURE BY</th>
                                <th>CONFIGURE DATE</th>
                                <th>DEPLOY BY</th>
                                <th>DEPLOY DATE</th>
                                <th>ROLL-OUT BY</th>
                                <th>ROLL-OUT DATE</th>
                                <th>APP. VERSION</th>
                                <th>REMARKS-2</th>
                            </tr>
                        </thead>
                        <tbody id="withdrawnDetailsListBody">
                            <!-- Withdrawn terminal rows will be inserted here by JavaScript -->
                        </tbody>
                    </table>
                    <p id="noDetailedWithdrawnTerminalsMsg" class="text-gray-500 text-center py-4 hidden">NO DETAILED WITHDRAWN TERMINALS TO DISPLAY.</p>
                </div>
            </div>

            <!-- Manual Status Update Section -->
            <div class="card">
                <h2 class="text-2xl font-bold text-gray-800 mb-4">UPDATE TERMINAL STATUS</h2>
                <div class="flex flex-col sm:flex-row items-center gap-4">
                    <div>
                        <label for="statusUpdateTidInput" class="block text-sm font-medium text-gray-700">TERMINAL ID (TID):</label>
                        <input type="text" id="statusUpdateTidInput" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" placeholder="E.G., T001">
                    </div>
                    <div>
                        <label for="statusUpdateSelect" class="block text-sm font-medium text-gray-700">SET STATUS:</label>
                        <select id="statusUpdateSelect" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                            <option value="">-- SELECT STATUS --</option>
                            <option value="live">LIVE</option>
                            <option value="withdrawn">WITHDRAWN</option>
                        </select>
                    </div>
                    <button id="updateStatusOnlyBtn" class="btn btn-primary mt-auto w-full sm:w-auto">UPDATE STATUS</button>
                </div>
            </div>

            <!-- Manual Other Details Update Section -->
            <div class="card">
                <h2 class="text-2xl font-bold text-gray-800 mb-4">UPDATE OTHER TERMINAL DETAILS</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div>
                        <label for="detailsUpdateTidInput" class="block text-sm font-medium text-gray-700">TERMINAL ID(S) (TID):</label>
                        <textarea id="detailsUpdateTidInput" rows="3" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" placeholder="ENTER TIDS, ONE PER LINE OR COMMA-SEPARATED"></textarea>
                    </div>
                    <!-- Empty div for grid alignment -->
                    <div></div>
                    <div>
                        <label for="configureByInput" class="block text-sm font-medium text-gray-700">CONFIGURE BY:</label>
                        <input type="text" id="configureByInput" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                    </div>
                    <div>
                        <label for="configureDateInput" class="block text-sm font-medium text-gray-700">CONFIGURE DATE:</label>
                        <input type="date" id="configureDateInput" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                    </div>
                    <div>
                        <label for="deployByInput" class="block text-sm font-medium text-gray-700">DEPLOY BY:</label>
                        <input type="text" id="deployByInput" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                    </div>
                    <div>
                        <label for="deployDateInput" class="block text-sm font-medium text-gray-700">DEPLOY DATE:</label>
                        <input type="date" id="deployDateInput" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                    </div>
                    <div>
                        <label for="rolloutByInput" class="block text-sm font-medium text-gray-700">ROLL-OUT BY:</label>
                        <input type="text" id="rolloutByInput" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                    </div>
                    <div>
                        <label for="rolloutDateInput" class="block text-sm font-medium text-gray-700">ROLL-OUT DATE:</label>
                        <input type="date" id="rolloutDateInput" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                    </div>
                    <div>
                        <label for="appVersionInput" class="block text-sm font-medium text-gray-700">APP. VERSION:</label>
                        <input type="text" id="appVersionInput" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                    </div>
                    <div class="md:col-span-2">
                        <label for="remarks2Input" class="block text-sm font-medium text-gray-700">REMARKS-2:</label>
                        <textarea id="remarks2Input" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm h-20"></textarea>
                    </div>
                </div>
                <button id="updateOtherDetailsBtn" class="btn btn-primary mt-6 w-full">UPDATE OTHER DETAILS</button>
            </div>

            <!-- Data Import Section - Only Excel Upload -->
            <div class="card">
                <h2 class="text-2xl font-bold text-gray-800 mb-4">IMPORT TERMINAL DATA</h2>
                <p class="text-gray-700 mb-2">
                    UPLOAD AN EXCEL FILE (.XLSX, .XLS) TO IMPORT TERMINAL DETAILS.
                    <strong class="text-red-600">IMPORTANT: THE COLUMN HEADERS IN YOUR EXCEL FILE MUST EXACTLY MATCH (CASE-SENSITIVE) THE HEADERS IN THE TABLE ABOVE.</strong>
                </p>
                <p class="text-sm text-blue-700 mb-4">
                    <strong class="font-semibold">NOTE ON STATUS:</strong> ALL TERMINALS IMPORTED FROM EXCEL WILL INITIALLY BE SET AS 'LIVE'. YOU CAN THEN USE THE 'MANUAL TERMINAL DETAILS UPDATE' SECTION TO CHANGE THEIR STATUS TO 'WITHDRAWN' OR UPDATE OTHER DETAILS.
                    <br>
                    <strong class="font-semibold text-red-700">IMPORTANT FOR APP. VERSION:</strong> THE 'APP. VERSION' WILL ONLY BE UPDATED IF BOTH 'ROLL-OUT BY' AND 'ROLL-OUT DATE' FIELDS ARE PROVIDED IN THE MANUAL UPDATE FORM. IF THEY ARE BLANK, THE 'APP. VERSION' WILL NOT BE CHANGED.
                </p>
                <label for="excelFileInput" class="file-upload-label w-full sm:w-auto">UPLOAD EXCEL FILE</label>
                <input type="file" id="excelFileInput" class="file-input" accept=".xlsx, .xls">
                <span id="fileNameDisplay" class="ml-2 text-gray-600"></span>
            </div>

            <!-- Merge Data Section -->
            <div class="card">
                <h2 class="text-2xl font-bold text-gray-800 mb-4">MERGE DATA FROM SECOND EXCEL FILE</h2>
                <p class="text-gray-700 mb-2">
                    UPLOAD A SECOND EXCEL FILE (.XLSX, .XLS) TO MERGE ITS DATA WITH THE EXISTING TERMINALS.
                    EXISTING TERMINALS WITH MATCHING TIDS WILL BE UPDATED; NEW TIDS WILL BE ADDED.
                    <strong class="text-red-600">IMPORTANT: COLUMN HEADERS MUST MATCH EXACTLY.</strong>
                </p>
                <p class="text-sm text-blue-700 mb-4">
                    <strong class="font-semibold">MERGE RULES:</strong>
                    <ul class="list-disc list-inside ml-4">
                        <li>FOR `TID`: IF THIS COLUMN IS PRESENT IN THE UPLOADED FILE, ITS VALUE WILL **ALWAYS OVERWRITE** EXISTING DATA, EVEN IF THE CELL IS BLANK.</li>
                        <li>FOR ALL OTHER FIELDS (`MID`, `MERCHANT NAME`, `DBA NAME`, `ADDRESS`, `BANK CONT. PERSON NAME`, `BANK CONT. PERSON NUMBER`, `DISTRICT`, `DIVISION`, `ZONE`, `POS S/N`, `POS BRAND & MODEL`, `OPERATOR NAME`, `SIM NUMBER`, `SIM IP`, `HOST IP`, `HOST PORT`, `VENDOR NAME`, `EMI`, `TENUR`, `REMARKS`, `CONFIGURE BY`, `CONFIGURE DATE`, `DEPLOY BY`, `DEPLOY DATE`, `ROLL-OUT BY`, `ROLL-OUT DATE`, `REMARKS-2`): BLANK FIELDS IN THE UPLOADED FILE WILL **NOT** OVERWRITE EXISTING DATA. ONLY CELLS WITH VALUES WILL UPDATE CORRESPONDING FIELDS.</li>
                        <li>`APP. VERSION` WILL ONLY UPDATE IF A VALUE IS PROVIDED IN THE UPLOADED FILE *AND* BOTH `ROLL-OUT BY` AND `ROLL-OUT DATE` ARE ALSO PROVIDED IN THE *UPLOADED FILE* FOR THAT SPECIFIC TERMINAL. IF `APP. VERSION` IS BLANK IN THE UPLOADED FILE, IT WILL NOT CLEAR THE EXISTING VALUE.</li>
                        <li>NEW TERMINALS (TIDS NOT FOUND) WILL BE ADDED AND DEFAULT TO 'LIVE' STATUS.</li>
                    </ul>
                </p>
                <label for="mergeExcelFileInput" class="file-upload-label w-full sm:w-auto">UPLOAD SECOND EXCEL FILE</label>
                <input type="file" id="mergeExcelFileInput" class="file-input" accept=".xlsx, .xls">
                <span id="mergeFileNameDisplay" class="ml-2 text-gray-600"></span>
                <button id="mergeDataBtn" class="btn btn-primary mt-4 w-full sm:w-auto">MERGE DATA</button>
            </div>
        </div>

        <!-- Removed: Configuration Generator Section -->
        <!-- <div id="configGenerator" class="main-section hidden-section"> ... </div> -->

    </div>

    <!-- Modal Structure -->
    <div id="terminalInfoModal" class="modal-overlay">
        <div class="modal-content">
            <button class="modal-close-btn" id="closeModalBtn">&times;</button>
            <h3 class="text-xl font-bold text-gray-800 mb-4">TERMINAL INFORMATION</h3>
            <div class="modal-field">
                <label>TID:</label>
                <span id="modalTID"></span>
            </div>
            <div class="modal-field">
                <label>DBA NAME:</label>
                <span id="modalDBAName"></span>
            </div>
            <div class="modal-field">
                <label>ADDRESS:</label>
                <span id="modalAddress"></span>
            </div>
            <button id="copyInfoBtn" class="btn btn-primary mt-4">COPY INFO</button>
            <span id="copyMessage" class="ml-2 text-sm text-green-600 hidden">COPIED!</span>
        </div>
    </div>

    <!-- XLSX Library CDN -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>

    <script>
        // Array to store terminal data for the dashboard
        let terminals = [];

        // Define the new header keys in order for mapping for the dashboard
        const newHeaders = [
            "S/N", "TID", "MID", "MERCHANT NAME", "DBA NAME", "ADDRESS", "BANK CONT. PERSON NAME",
            "BANK CONT. PERSON NUMBER", "DISTRICT", "DIVISION", "ZONE", "POS S/N",
            "POS BRAND & MODEL", "OPERATOR NAME", "SIM NUMBER", "SIM IP", "HOST IP",
            "HOST PORT", "VENDOR NAME", "EMI", "TENUR", "REMARKS", "CONFIGURE BY",
            "CONFIGURE DATE", "DEPLOY BY", "DEPLOY DATE", "ROLL-OUT BY", "ROLL-OUT DATE",
            "APP. VERSION", "REMARKS-2"
        ];

        // Dummy data for initial display, adjusted to new headers
        const dummyData = [
            {
                "S/N": "1", "TID": "T001", "MID": "M001", "MERCHANT NAME": "Alpha Store", "DBA NAME": "Alpha Retail",
                "ADDRESS": "123 Main St, Central City, Dhaka, Bangladesh.", "BANK CONT. PERSON NAME": "John Doe",
                "BANK CONT. PERSON NUMBER": "1234567890", "DISTRICT": "Central", "DIVISION": "Dhaka",
                "ZONE": "Zone A", "POS S/N": "POS1001", "POS BRAND & MODEL": "Verifone VX520",
                "OPERATOR NAME": "Ops A", "SIM NUMBER": "SIM1001", "SIM IP": "192.168.1.1",
                "HOST IP": "203.0.113.1", "HOST PORT": "8080", "VENDOR NAME": "Vendor X", "EMI": "Yes",
                "TENUR": "12 Months", "REMARKS": "Good condition", "CONFIGURE BY": "Config User 1",
                "CONFIGURE DATE": "2025-07-10", "DEPLOY BY": "Deploy User 1", "DEPLOY DATE": "2025-07-11",
                "ROLL-OUT BY": "Rollout User 1", "ROLL-OUT DATE": "2025-07-12", "APP. VERSION": "1.0.0",
                "REMARKS-2": "Initial live status"
            },
            {
                "S/N": "2", "TID": "T002", "MID": "M002", "MERCHANT NAME": "Beta Shop", "DBA NAME": "Beta Goods",
                "ADDRESS": "456 Oak Ave, East Town, Chittagong, Bangladesh.", "BANK CONT. PERSON NAME": "Jane Smith",
                "BANK CONT. PERSON NUMBER": "0987654321", "DISTRICT": "East", "DIVISION": "Chittagong",
                "ZONE": "Zone B", "POS S/N": "POS1002", "POS BRAND & MODEL": "Ingenico ICT220",
                "OPERATOR NAME": "Ops B", "SIM NUMBER": "SIM1002", "SIM IP": "192.168.1.2",
                "HOST IP": "203.0.113.2", "HOST PORT": "8080", "VENDOR NAME": "Vendor Y", "EMI": "No",
                "TENUR": "N/A", "REMARKS": "Stable", "CONFIGURE BY": "Config User 2",
                "CONFIGURE DATE": "2025-07-09", "DEPLOY BY": "Deploy User 2", "DEPLOY DATE": "2025-07-10",
                "ROLL-OUT BY": "Rollout User 2", "ROLL-OUT DATE": "2025-07-11", "APP. VERSION": "1.1.0",
                "REMARKS-2": "Initial live status"
            },
            {
                "S/N": "3", "TID": "T003", "MID": "M003", "MERCHANT NAME": "Gamma Mart", "DBA NAME": "Gamma Sales",
                "ADDRESS": "789 Pine Ln, West Village, Rajshahi, Bangladesh.", "BANK CONT. PERSON NAME": "Mike Johnson",
                "BANK CONT. PERSON NUMBER": "1122334455", "DISTRICT": "West", "DIVISION": "Rajshahi",
                "ZONE": "Zone C", "POS S/N": "POS1003", "POS BRAND & MODEL": "Pax S80",
                "OPERATOR NAME": "Ops C", "SIM NUMBER": "SIM1003", "SIM IP": "192.168.1.3",
                "HOST IP": "203.0.113.3", "HOST PORT": "8080", "VENDOR NAME": "Vendor Z", "EMI": "Yes",
                "TENUR": "6 Months", "REMARKS": "Due for upgrade", "CONFIGURE BY": "Config User 3",
                "CONFIGURE DATE": "2025-07-08", "DEPLOY BY": "Deploy User 3", "DEPLOY DATE": "2025-07-09",
                "ROLL-OUT BY": "Rollout User 3", "ROLL-OUT DATE": "2025-07-10", "APP. VERSION": "1.0.0",
                "REMARKS-2": "Initial live status"
            }
        ];

        /**
         * Converts an Excel date number to a YYYY-MM-DD string.
         * Handles cases where the input might not be a number or is already a date string.
         * @param {any} excelDate - The value from an Excel cell.
         * @returns {string} The date in YYYY-MM-DD format, or an empty string if invalid.
         */
        function excelDateToJSDate(excelDate) {
            if (typeof excelDate === 'number' && excelDate > 0) {
                // Excel's epoch is Jan 1, 1900. JavaScript's is Jan 1, 1970.
                // 25569 is the number of days between 1900-01-01 and 1970-01-01.
                // 86400000 is milliseconds in a day.
                const date = new Date(Math.round((excelDate - 25569) * 86400 * 1000));
                // Check if the date is valid
                if (!isNaN(date.getTime())) {
                    return date.toISOString().split('T')[0];
                }
            } else if (typeof excelDate === 'string') {
                // Attempt to parse as a date string (e.g., "2025-01-01")
                const date = new Date(excelDate);
                if (!isNaN(date.getTime())) {
                    return date.toISOString().split('T')[0];
                }
            }
            return ''; // Return empty string for invalid or non-date values
        }

        /**
         * Formats a YYYY-MM-DD date string to D-Mon-YY (e.g., 8-Jan-25).
         * @param {string} dateString - The date string in YYYY-MM-DD format.
         * @returns {string} The formatted date string, or the original string if invalid.
         */
        function formatDateToDMonYY(dateString) {
            if (!dateString) return '';
            const date = new Date(dateString);
            if (isNaN(date.getTime())) {
                return dateString; // Return original if invalid date
            }

            const day = date.getDate();
            const monthNames = ["Jan", "Feb", "Mar", "Apr", "May", "Jun",
                                "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
            const month = monthNames[date.getMonth()];
            const year = String(date.getFullYear()).slice(-2); // Get last two digits of the year

            return `${day}-${month}-${year}`;
        }


        /**
         * Renders all terminal data to the various sections of the dashboard.
         * @param {string} searchTerm - Optional search term to filter live terminals.
         */
        function renderTerminals(searchTerm = '') {
            // Get references to HTML elements
            const totalTerminalsEl = document.getElementById('totalTerminals');
            const liveTerminalsEl = document.getElementById('liveTerminals');
            const withdrawnTerminalsEl = document.getElementById('withdrawnTerminals');
            const appVersionBreakdownEl = document.getElementById('appVersionBreakdown');
            const liveTerminalListBodyEl = document.getElementById('liveTerminalListBody');
            const withdrawnDetailsListBodyEl = document.getElementById('withdrawnDetailsListBody');
            const noDetailedWithdrawnTerminalsMsgEl = document.getElementById('noDetailedWithdrawnTerminalsMsg');


            // Filter terminals into live and withdrawn based on their 'status' property
            const liveTerminals = terminals.filter(t => t.status === 'live');
            const withdrawnTerminals = terminals.filter(t => t.status === 'withdrawn');

            // Calculate counts
            const totalCount = terminals.length;
            const liveCount = liveTerminals.length;
            const withdrawnCount = withdrawnTerminals.length;


            // Update overview counts
            totalTerminalsEl.textContent = totalCount;
            liveTerminalsEl.textContent = liveCount;
            withdrawnTerminalsEl.textContent = withdrawnCount;

            // Calculate app version breakdown based on the 'APP. VERSION' field
            const appVersions = {};
            terminals.forEach(t => {
                const version = t["APP. VERSION"];
                if (version) {
                    appVersions[version] = (appVersions[version] || 0) + 1;
                }
            });

            // Render app version breakdown
            appVersionBreakdownEl.innerHTML = ''; // Clear previous content
            if (Object.keys(appVersions).length === 0) {
                appVersionBreakdownEl.innerHTML = '<p class="text-gray-500">NO APP VERSION DATA AVAILABLE.</p>';
            } else {
                for (const version in appVersions) {
                    const versionCard = `
                        <div class="bg-purple-100 p-4 rounded-lg shadow-md">
                            <p class="text-lg font-semibold text-purple-800">APP VERSION ${version}</p>
                            <p class="text-4xl font-bold text-purple-600 mt-2">${appVersions[version]}</p>
                        </div>
                    `;
                    appVersionBreakdownEl.insertAdjacentHTML('beforeend', versionCard);
                }
            }


            // Render Live Terminal Details with search filter
            liveTerminalListBodyEl.innerHTML = ''; // Clear previous content
            const lowerCaseSearchTerm = searchTerm.toLowerCase();
            const filteredLiveTerminals = liveTerminals.filter(terminal => {
                if (lowerCaseSearchTerm === '') return true; // Show all if search term is empty

                // Check all relevant string fields for the search term
                return newHeaders.some(header => {
                    if (header === "S/N") return false; // S/N is dynamic, not part of data to search

                    let valueToSearch = terminal[header] || '';
                    if (header === "CONFIGURE DATE") {
                        // Search on the displayed format for CONFIGURE DATE
                        valueToSearch = formatDateToDMonYY(valueToSearch);
                    }
                    return String(valueToSearch).toLowerCase().includes(lowerCaseSearchTerm);
                });
            });

            if (filteredLiveTerminals.length === 0) {
                liveTerminalListBodyEl.innerHTML = `<tr><td colspan="${newHeaders.length}" class="text-center text-gray-500 py-4">NO LIVE TERMINAL DATA FOUND MATCHING "${searchTerm}".</td></tr>`;
            } else {
                filteredLiveTerminals.forEach((terminal, index) => {
                    let rowHtml = '<tr>';
                    newHeaders.forEach(header => {
                        let cellContent;
                        let statusClass = '';

                        if (header === 'S/N') {
                            cellContent = index + 1;
                        } else if (header === 'TID') {
                            cellContent = `<span class="font-bold text-indigo-700">${(terminal[header] || '').toUpperCase()}</span>`;
                        } else if (header === 'REMARKS-2') {
                            let statusText = 'UNKNOWN';
                            statusClass = 'bg-gray-100 text-gray-800';
                            if (terminal.status === 'live') {
                                statusText = 'LIVE';
                                statusClass = 'bg-green-100 text-green-800';
                            } else if (terminal.status === 'withdrawn') {
                                statusText = 'WITHDRAWN';
                                statusClass = 'bg-red-100 text-red-800';
                            }
                            cellContent = `${(terminal[header] || '').toUpperCase()} <span class="px-2 py-1 rounded-full text-xs font-semibold ${statusClass}">${statusText}</span>`;
                        } else if (header === "CONFIGURE DATE") {
                            cellContent = formatDateToDMonYY(terminal[header]);
                        }
                        else {
                            cellContent = (terminal[header] || '').toUpperCase();
                        }
                        rowHtml += `<td>${cellContent}</td>`;
                    });
                    rowHtml += '</tr>';
                    liveTerminalListBodyEl.insertAdjacentHTML('beforeend', rowHtml);
                });
            }


            // Render Withdrawn Terminal Details (no search filter for this section)
            withdrawnDetailsListBodyEl.innerHTML = ''; // Clear previous content
            if (withdrawnTerminals.length === 0) {
                noDetailedWithdrawnTerminalsMsgEl.classList.remove('hidden');
                withdrawnDetailsListBodyEl.innerHTML = `<tr><td colspan="${newHeaders.length}" class="text-center text-gray-500 py-4">NO DETAILED WITHDRAWN TERMINALS TO DISPLAY.</td></tr>`;
            } else {
                withdrawnTerminals.forEach((terminal, index) => { // Added index for S/N
                    let rowHtml = '<tr>';
                    newHeaders.forEach(header => {
                        let cellContent;
                        let statusClass = '';

                        if (header === 'S/N') { // Dynamically set S/N for withdrawn table
                            cellContent = index + 1;
                        } else if (header === 'TID') {
                            cellContent = `<span class="font-bold text-indigo-700">${(terminal[header] || '').toUpperCase()}</span>`;
                        } else if (header === 'REMARKS-2') {
                            let statusText = 'UNKNOWN';
                            statusClass = 'bg-gray-100 text-gray-800';
                            if (terminal.status === 'live') {
                                statusText = 'LIVE';
                                statusClass = 'bg-green-100 text-green-800';
                            } else if (terminal.status === 'withdrawn') {
                                statusText = 'WITHDRAWN';
                                statusClass = 'bg-red-100 text-red-800';
                            }
                            cellContent = `${(terminal[header] || '').toUpperCase()} <span class="px-2 py-1 rounded-full text-xs font-semibold ${statusClass}">${statusText}</span>`;
                        } else if (header === "CONFIGURE DATE") {
                            cellContent = formatDateToDMonYY(terminal[header]);
                        }
                        else {
                            cellContent = (terminal[header] || '').toUpperCase();
                        }
                        rowHtml += `<td>${cellContent}</td>`;
                    });
                    rowHtml += '</tr>';
                    withdrawnDetailsListBodyEl.insertAdjacentHTML('beforeend', rowHtml);
                });
            }
        }

        /**
         * Processes the imported JSON data from Excel and updates the terminals array.
         * This function replaces the existing data.
         * @param {Array<Object>} data - An array of objects, where each object represents a row
         * and keys are column headers from the Excel file.
         */
        function processImportedData(data) {
            console.log("Processing initial import data:", data); // Debugging log
            const newTerminals = [];

            data.forEach(row => {
                const terminal = {};
                let isValidRow = true;

                newHeaders.forEach(header => {
                    let value = row[header] !== undefined ? row[header] : ''; // Don't trim immediately for date conversion

                    // Apply date conversion for CONFIGURE DATE
                    if (header === "CONFIGURE DATE") {
                        // Check both "CONFIGURE DATE" and "CONFIGURATION DATE"
                        const val1 = row["CONFIGURE DATE"] !== undefined ? row["CONFIGURE DATE"] : '';
                        const val2 = row["CONFIGURATION DATE"] !== undefined ? row["CONFIGURATION DATE"] : '';
                        value = val1 !== '' ? val1 : val2; // Prefer CONFIGURE DATE, then CONFIGURATION DATE
                        value = excelDateToJSDate(value); // Convert to YYYY-MM-DD
                    } else {
                        value = String(value).trim(); // Trim other values
                    }

                    terminal[header] = value;
                });

                // Basic validation: Check if TID is present
                if (!terminal["TID"]) {
                    console.warn(`Skipping row due to missing TID:`, row);
                    isValidRow = false;
                }

                if (isValidRow) {
                    // All terminals are initially set to 'live' upon import
                    terminal.status = 'live';
                    // 'APP. VERSION' directly from the column
                    terminal.appVersion = terminal["APP. VERSION"] || 'N/A';

                    newTerminals.push(terminal);
                    console.log(`Imported Terminal: TID=${terminal["TID"]}, Initial Status=${terminal.status}`); // Log initial status
                }
            });

            terminals = newTerminals; // Replace existing terminals with imported data
            renderTerminals(); // Re-render the dashboard
            showMessage('TERMINAL DATA IMPORTED SUCCESSFULLY! ALL TERMINALS INITIALLY SET TO LIVE.', 'success');
        }

        /**
         * Merges new data from an Excel file into the existing terminals array.
         * @param {Array<Object>} newData - An array of objects from the second Excel file.
         */
        function mergeExcelData(newData) {
            console.log("Starting merge operation with new data:", newData); // Debugging log
            let updatedCount = 0;
            let addedCount = 0;
            let appVersionSkippedTids = [];

            newData.forEach(incomingTerminal => {
                const incomingTID = incomingTerminal["TID"] ? String(incomingTerminal["TID"]).trim() : '';
                console.log(`Processing incoming terminal with TID: '${incomingTID}'`, incomingTerminal); // Debugging log

                if (!incomingTID) {
                    console.warn("Skipping incoming row due to missing TID:", incomingTerminal);
                    return; // Skip this row if TID is missing
                }

                let terminalToUpdate = null;
                let foundByIndex = -1;

                // Only try to find by TID
                if (incomingTID) {
                    foundByIndex = terminals.findIndex(t => t["TID"] === incomingTID);
                    if (foundByIndex !== -1) {
                        terminalToUpdate = terminals[foundByIndex];
                        console.log(`Found existing terminal for TID '${incomingTID}' at index ${foundByIndex}.`); // Debugging log
                    } else {
                        console.log(`No existing terminal found for TID '${incomingTID}'. Will add as new.`); // Debugging log
                    }
                }

                if (terminalToUpdate) {
                    // Terminal exists (found by TID), update it
                    updatedCount++;

                    // Always set status to 'live' if found via merge
                    terminalToUpdate.status = 'live';

                    newHeaders.forEach(header => {
                        // Skip S/N as it's auto-generated for display
                        if (header === "S/N") return;

                        let incomingValue;
                        if (header === "CONFIGURE DATE") {
                            const val1 = incomingTerminal["CONFIGURE DATE"] !== undefined ? incomingTerminal["CONFIGURE DATE"] : '';
                            const val2 = incomingTerminal["CONFIGURATION DATE"] !== undefined ? incomingTerminal["CONFIGURATION DATE"] : '';
                            incomingValue = val1 !== '' ? val1 : val2;
                            incomingValue = excelDateToJSDate(incomingValue); // Convert to YYYY-MM-DD
                        } else {
                            incomingValue = incomingTerminal[header] !== undefined ? String(incomingTerminal[header]).trim() : '';
                        }

                        if (header === "TID") {
                            // For TID, always overwrite, even with blank incoming values
                            terminalToUpdate[header] = incomingValue;
                            console.log(`Overwrote '${header}' for TID '${incomingTID}' with: '${incomingValue}'.`); // Debugging log
                        } else if (header === "APP. VERSION") {
                            const incomingRolloutBy = incomingTerminal["ROLL-OUT BY"] !== undefined ? String(incomingTerminal["ROLL-OUT BY"]).trim() : '';
                            const incomingRolloutDate = incomingTerminal["ROLL-OUT DATE"] !== undefined ? String(incomingTerminal["ROLL-OUT DATE"]).trim() : '';

                            if (incomingValue !== '') { // Only update if incoming value is NOT blank
                                if (incomingRolloutBy !== '' && incomingRolloutDate !== '') {
                                    terminalToUpdate[header] = incomingValue;
                                    console.log(`Updated '${header}' for TID '${incomingTID}': '${incomingValue}' (Roll-Out details present).`); // Debugging log
                                } else {
                                    appVersionSkippedTids.push(incomingTID);
                                    console.log(`Skipped updating '${header}' for TID '${incomingTID}': '${incomingValue}' (missing Roll-Out details).`); // Debugging log
                                }
                            }
                            // If incomingValue is '', do nothing (preserve existing)
                        } else {
                            // For all other fields, only update if incoming value is not blank
                            if (incomingValue !== '') {
                                terminalToUpdate[header] = incomingValue;
                                console.log(`Updated '${header}' for TID '${incomingTID}' with: '${incomingValue}'.`); // Debugging log
                            } else {
                                console.log(`Preserved existing '${header}' for TID '${incomingTID}' (incoming was blank).`); // Debugging log
                            }
                        }
                    });

                } else {
                    // Terminal does not exist (by TID), add it as a new terminal
                    addedCount++;
                    const newTerminal = {};
                    newHeaders.forEach(header => {
                        let value;
                        if (header === "CONFIGURE DATE") {
                            const val1 = incomingTerminal["CONFIGURE DATE"] !== undefined ? incomingTerminal["CONFIGURE DATE"] : '';
                            const val2 = incomingTerminal["CONFIGURATION DATE"] !== undefined ? incomingTerminal["CONFIGURATION DATE"] : '';
                            value = val1 !== '' ? val1 : val2;
                            value = excelDateToJSDate(value); // Convert to YYYY-MM-DD
                        } else {
                            value = incomingTerminal[header] !== undefined ? String(incomingTerminal[header]).trim() : '';
                        }
                        newTerminal[header] = value;
                    });
                    newTerminal.status = 'live'; // New terminals default to live
                    newTerminal.appVersion = newTerminal["APP. VERSION"] || 'N/A';
                    terminals.push(newTerminal);
                    console.log(`Added new terminal: TID=${newTerminal["TID"]}`); // Debugging log
                }
            });

            renderTerminals(); // Re-render the dashboard after all merges

            let message = `MERGE COMPLETE: ${updatedCount} TERMINAL(S) UPDATED, ${addedCount} NEW TERMINAL(S) ADDED.`;
            if (appVersionSkippedTids.length > 0) {
                message += ` APP. VERSION SKIPPED FOR: ${appVersionSkippedTids.join(', ')} (MISSING ROLL-OUT DETAILS IN MERGED FILE).`;
            }
            showMessage(message, (updatedCount > 0 || addedCount > 0) ? 'success' : 'warning');
            console.log("FINAL TERMINALS ARRAY AFTER MERGE:", terminals); // Debugging log
        }


        /**
         * Updates the details of a terminal based on its TID.
         * This function is used for manual updates from the form.
         * @param {string} tid - The Terminal ID to update.
         * @param {object} updates - An object containing the fields to update.
         * @returns {object} An object indicating if the terminal was found and if APP. VERSION update was skipped.
         */
        function updateTerminalDetails(tid, updates) {
            const terminalIndex = terminals.findIndex(t => t["TID"] === tid);

            if (terminalIndex !== -1) {
                const terminal = terminals[terminalIndex];
                let appVersionUpdateSkipped = false;

                // Update status if provided and not blank
                if (updates.status !== undefined && updates.status !== '') {
                    terminal.status = updates.status;
                }

                // Update fields only if the new value is explicitly provided AND not blank.
                // If the update value is blank, the existing data is preserved.
                if (updates.configureBy !== undefined && updates.configureBy !== '') terminal["CONFIGURE BY"] = updates.configureBy;
                // CONFIGURE DATE from manual input is already YYYY-MM-DD
                if (updates.configureDate !== undefined && updates.configureDate !== '') terminal["CONFIGURE DATE"] = updates.configureDate;
                if (updates.deployBy !== undefined && updates.deployBy !== '') terminal["DEPLOY BY"] = updates.deployBy;
                if (updates.deployDate !== undefined && updates.deployDate !== '') terminal["DEPLOY DATE"] = updates.deployDate;
                if (updates.rolloutBy !== undefined && updates.rolloutBy !== '') terminal["ROLL-OUT BY"] = updates.rolloutBy;
                if (updates.rolloutDate !== undefined && updates.rolloutDate !== '') terminal["ROLL-OUT DATE"] = updates.rolloutDate;
                if (updates.remarks2 !== undefined && updates.remarks2 !== '') terminal["REMARKS-2"] = updates.remarks2;

                // Conditional update for APP. VERSION
                if (updates.appVersion !== undefined) { // Check if appVersion was provided in the form (can be empty string)
                    // Only update APP. VERSION if ROLL-OUT BY and ROLL-OUT DATE are NOT blank
                    if (updates.rolloutBy === '' || updates.rolloutDate === '') {
                        appVersionUpdateSkipped = true;
                    } else {
                        terminal["APP. VERSION"] = updates.appVersion; // Update APP. VERSION (can be cleared if appVersion is '')
                    }
                }
                return { found: true, appVersionSkipped: appVersionUpdateSkipped };
            } else {
                return { found: false, appVersionSkipped: false };
            }
        }


        /**
         * Displays a temporary message to the user.
         * @param {string} message - The message to display.
         * @param {'success'|'error'|'warning'} type - The type of message.
         */
        function showMessage(message, type) {
            const messageBox = document.createElement('div');
            messageBox.textContent = message;
            messageBox.className = `fixed bottom-4 right-4 p-4 rounded-lg shadow-lg text-white z-50 transition-opacity duration-300 ${
                type === 'success' ? 'bg-green-500' :
                type === 'error' ? 'bg-red-500' :
                'bg-yellow-500'
            }`;
            document.body.appendChild(messageBox);

            setTimeout(() => {
                messageBox.style.opacity = '0';
                messageBox.addEventListener('transitionend', () => messageBox.remove());
            }, 3000); // Message disappears after 3 seconds
        }


        // Event Listeners for Terminal Management Dashboard
        document.addEventListener('DOMContentLoaded', () => {
            // Initialize with dummy data as there's no persistence
            terminals = dummyData;
            terminals.forEach(t => {
                t.status = 'live'; // Ensure dummy data has status
                if (t["REMARKS-2"] && t["REMARKS-2"].toLowerCase().includes("withdrawn")) {
                    t.status = "withdrawn";
                }
            });
            renderTerminals(); // Initial render without search term

            // Excel file input change handler for initial upload
            const excelFileInput = document.getElementById('excelFileInput');
            const fileNameDisplay = document.getElementById('fileNameDisplay');

            excelFileInput.addEventListener('change', (event) => {
                const file = event.target.files[0];
                if (file) {
                    fileNameDisplay.textContent = file.name;
                    const reader = new FileReader();

                    reader.onload = (e) => {
                        try {
                            const data = new Uint8Array(e.target.result);
                            const workbook = XLSX.read(data, { type: 'array' });

                            // Assuming the first sheet contains the data
                            const firstSheetName = workbook.SheetNames[0];
                            const worksheet = workbook.Sheets[firstSheetName];

                            // Convert sheet to array of JSON objects
                            const finalJsonData = XLSX.utils.sheet_to_json(worksheet);


                            if (finalJsonData.length === 0) {
                                showMessage('THE SELECTED EXCEL FILE IS EMPTY OR CONTAINS NO READABLE DATA.', 'warning');
                                return;
                            }

                            // Process the imported JSON data (replaces existing data)
                            processImportedData(finalJsonData);

                            // Clear the file input so the same file can be re-uploaded if needed
                            excelFileInput.value = '';
                            fileNameDisplay.textContent = ''; // Clear file name display
                        } catch (error) {
                            console.error('ERROR READING EXCEL FILE:', error);
                            showMessage('ERROR PROCESSING EXCEL FILE. PLEASE ENSURE IT\'S A VALID .XLSX OR .XLS FORMAT AND CONTAINS DATA.', 'error');
                        }
                    };

                    reader.onerror = (error) => {
                        console.error('FileReader error:', error);
                        showMessage('ERROR READING FILE. PLEASE TRY AGAIN.', 'error');
                    };

                    reader.readAsArrayBuffer(file);
                } else {
                    fileNameDisplay.textContent = ''; // Clear file name if no file selected
                }
            });

            // Manual Status Update button handler
            document.getElementById('updateStatusOnlyBtn').addEventListener('click', () => {
                const tid = document.getElementById('statusUpdateTidInput').value.trim();
                const status = document.getElementById('statusUpdateSelect').value;

                if (tid) {
                    const updates = {
                        status: status
                    };
                    const result = updateTerminalDetails(tid, updates);
                    if (result.found) {
                        showMessage(`TERMINAL ${tid} STATUS UPDATED TO ${status.charAt(0).toUpperCase() + status.slice(1)}.`, 'success');
                    } else {
                        showMessage(`TERMINAL WITH TID ${tid} NOT FOUND.`, 'error');
                    }
                    renderTerminals(); // Re-render after single status update
                    // Clear input fields after update
                    document.getElementById('statusUpdateTidInput').value = '';
                    document.getElementById('statusUpdateSelect').value = '';
                } else {
                    showMessage('PLEASE ENTER A TERMINAL ID TO UPDATE STATUS.', 'warning');
                }
            });

            // Manual Other Details Update button handler
            document.getElementById('updateOtherDetailsBtn').addEventListener('click', () => {
                const tidInput = document.getElementById('detailsUpdateTidInput').value.trim();
                const tids = tidInput.split(/[\s,]+/).filter(id => id !== ''); // Split by space or comma, filter empty

                if (tids.length === 0) {
                    showMessage('PLEASE ENTER AT LEAST ONE TERMINAL ID TO UPDATE OTHER DETAILS.', 'warning');
                    return;
                }

                const configureBy = document.getElementById('configureByInput').value.trim();
                const configureDate = document.getElementById('configureDateInput').value.trim();
                const deployBy = document.getElementById('deployByInput').value.trim();
                const deployDate = document.getElementById('deployDateInput').value.trim();
                const rolloutBy = document.getElementById('rolloutByInput').value.trim();
                const rolloutDate = document.getElementById('rolloutDateInput').value.trim();
                const appVersion = document.getElementById('appVersionInput').value.trim();
                const remarks2 = document.getElementById('remarks2Input').value.trim();

                const updates = {
                    configureBy: configureBy,
                    configureDate: configureDate,
                    deployBy: deployBy,
                    deployDate: deployDate,
                    rolloutBy: rolloutBy,
                    rolloutDate: rolloutDate,
                    appVersion: appVersion,
                    remarks2: remarks2
                };

                let updatedCount = 0;
                let notFoundTids = [];
                let appVersionSkippedTids = [];

                tids.forEach(tid => {
                    const result = updateTerminalDetails(tid, updates);
                    if (result.found) {
                        updatedCount++;
                        if (result.appVersionSkipped) {
                            appVersionSkippedTids.push(tid);
                        }
                    } else {
                        notFoundTids.push(tid);
                    }
                });

                renderTerminals(); // Re-render once after all batch updates

                // Provide comprehensive feedback
                let message = `${updatedCount} TERMINAL(S) UPDATED.`;
                if (notFoundTids.length > 0) {
                    message += ` NOT FOUND: ${notFoundTids.join(', ')}.`;
                }
                if (appVersionSkippedTids.length > 0) {
                    message += ` APP. VERSION SKIPPED FOR: ${appVersionSkippedTids.join(', ')} (MISSING ROLL-OUT DETAILS).`;
                }
                showMessage(message, updatedCount > 0 ? 'success' : 'error');

                // Clear input fields after update
                document.getElementById('detailsUpdateTidInput').value = '';
                document.getElementById('configureByInput').value = '';
                document.getElementById('configureDateInput').value = '';
                document.getElementById('deployByInput').value = '';
                document.getElementById('deployDateInput').value = '';
                document.getElementById('rolloutByInput').value = '';
                document.getElementById('rolloutDateInput').value = '';
                document.getElementById('appVersionInput').value = '';
                document.getElementById('remarks2Input').value = '';
            });

            // Merge Excel file input change handler
            const mergeExcelFileInput = document.getElementById('mergeExcelFileInput');
            const mergeFileNameDisplay = document.getElementById('mergeFileNameDisplay');
            const mergeDataBtn = document.getElementById('mergeDataBtn');

            mergeExcelFileInput.addEventListener('change', (event) => {
                const file = event.target.files[0];
                if (file) {
                    mergeFileNameDisplay.textContent = file.name;
                } else {
                    mergeFileNameDisplay.textContent = '';
                }
            });

            mergeDataBtn.addEventListener('click', () => {
                const file = mergeExcelFileInput.files[0];
                if (!file) {
                    showMessage('PLEASE SELECT A SECOND EXCEL FILE TO MERGE.', 'warning');
                    return;
                }

                const reader = new FileReader();
                reader.onload = (e) => {
                    try {
                        const data = new Uint8Array(e.target.result);
                        const workbook = XLSX.read(data, { type: 'array' });
                        const firstSheetName = workbook.SheetNames[0];
                        const worksheet = workbook.Sheets[firstSheetName];
                        const finalJsonData = XLSX.utils.sheet_to_json(worksheet);
                        console.log("Parsed data from second Excel file:", finalJsonData); // Debugging log

                        if (finalJsonData.length === 0) {
                            showMessage('THE SELECTED EXCEL FILE IS EMPTY OR CONTAINS NO READABLE DATA FOR MERGING.', 'warning');
                            return;
                        }

                        mergeExcelData(finalJsonData);

                        // Clear file inputs after merge
                        mergeExcelFileInput.value = '';
                        mergeFileNameDisplay.textContent = '';
                    } catch (error) {
                        console.error('ERROR READING MERGE EXCEL FILE:', error);
                        showMessage('ERROR PROCESSING MERGE EXCEL FILE. PLEASE ENSURE IT\'S A VALID .XLSX OR .XLS FORMAT AND CONTAINS DATA.', 'error');
                    }
                };
                reader.onerror = (error) => {
                    console.error('FileReader error during merge:', error);
                    showMessage('ERROR READING MERGE FILE. PLEASE TRY AGAIN.', 'error');
                };
                reader.readAsArrayBuffer(file);
            });

            // Live search functionality
            const liveSearchInput = document.getElementById('liveSearchInput');
            const liveSearchBtn = document.getElementById('liveSearchBtn');
            const terminalInfoModal = document.getElementById('terminalInfoModal');
            const modalTID = document.getElementById('modalTID');
            const modalDBAName = document.getElementById('modalDBAName');
            const modalAddress = document.getElementById('modalAddress');
            const copyInfoBtn = document.getElementById('copyInfoBtn');
            const copyMessage = document.getElementById('copyMessage');
            const closeModalBtn = document.getElementById('closeModalBtn');

            // Event listener for typing in the search input
            liveSearchInput.addEventListener('keyup', (event) => {
                renderTerminals(liveSearchInput.value);
            });

            // Event listener for clicking the search button
            liveSearchBtn.addEventListener('click', () => {
                const searchTerm = liveSearchInput.value;
                renderTerminals(searchTerm); // First, render the filtered table

                const liveTerminals = terminals.filter(t => t.status === 'live');
                const lowerCaseSearchTerm = searchTerm.toLowerCase();

                const filteredLiveTerminals = liveTerminals.filter(terminal => {
                    if (lowerCaseSearchTerm === '') return true;

                    return newHeaders.some(header => {
                        if (header === "S/N") return false;

                        let valueToSearch = terminal[header] || '';
                        if (header === "CONFIGURE DATE") {
                            valueToSearch = formatDateToDMonYY(valueToSearch);
                        }
                        return String(valueToSearch).toLowerCase().includes(lowerCaseSearchTerm);
                    });
                });

                if (filteredLiveTerminals.length > 0) {
                    const firstMatch = filteredLiveTerminals[0];
                    modalTID.textContent = (firstMatch["TID"] || 'N/A').toUpperCase();
                    modalDBAName.textContent = (firstMatch["DBA NAME"] || 'N/A').toUpperCase();
                    modalAddress.textContent = (firstMatch["ADDRESS"] || 'N/A').toUpperCase();
                    copyInfoBtn.classList.remove('hidden'); // Ensure copy button is visible
                    terminalInfoModal.classList.add('show');
                } else {
                    modalTID.textContent = 'N/A';
                    modalDBAName.textContent = 'NO TERMINAL FOUND MATCHING YOUR SEARCH.';
                    modalAddress.textContent = ''; // Clear address
                    copyInfoBtn.classList.add('hidden'); // Hide copy button if no match
                    terminalInfoModal.classList.add('show');
                }
            });

            // Copy Info Button functionality
            copyInfoBtn.addEventListener('click', () => {
                const tid = modalTID.textContent;
                const dbaName = modalDBAName.textContent;
                const address = modalAddress.textContent;
                const textToCopy = `TID: ${tid}\nDBA NAME: ${dbaName}\nADDRESS: ${address}`;

                // Use document.execCommand('copy') for better iframe compatibility
                const tempTextArea = document.createElement('textarea');
                tempTextArea.value = textToCopy;
                document.body.appendChild(tempTextArea);
                tempTextArea.select();
                try {
                    document.execCommand('copy');
                    copyMessage.classList.remove('hidden');
                    setTimeout(() => {
                        copyMessage.classList.add('hidden');
                    }, 2000); // Hide "Copied!" message after 2 seconds
                } catch (err) {
                    console.error('Failed to copy text: ', err);
                    showMessage('FAILED TO COPY INFORMATION.', 'error');
                } finally {
                    document.body.removeChild(tempTextArea);
                }
            });

            // Close Modal Button
            closeModalBtn.addEventListener('click', () => {
                terminalInfoModal.classList.remove('show');
                copyInfoBtn.classList.remove('hidden'); // Ensure copy button is visible for next time
            });

            // Close modal when clicking outside (on the overlay)
            terminalInfoModal.addEventListener('click', (event) => {
                if (event.target === terminalInfoModal) {
                    terminalInfoModal.classList.remove('show');
                    copyInfoBtn.classList.remove('hidden'); // Ensure copy button is visible for next time
                }
            });

            // Download button functionality
            const liveDownloadBtn = document.getElementById('liveDownloadBtn');
            liveDownloadBtn.addEventListener('click', () => {
                const currentSearchTerm = liveSearchInput.value;
                const liveTerminals = terminals.filter(t => t.status === 'live');
                const lowerCaseSearchTerm = currentSearchTerm.toLowerCase();

                // Filter data based on current search term, similar to renderTerminals
                const dataToExport = liveTerminals.filter(terminal => {
                    if (lowerCaseSearchTerm === '') return true; // Export all if no search term

                    return newHeaders.some(header => {
                        if (header === "S/N") return false;

                        let valueToSearch = terminal[header] || '';
                        if (header === "CONFIGURE DATE") {
                            valueToSearch = formatDateToDMonYY(valueToSearch); // Use displayed format for search
                        }
                        return String(valueToSearch).toLowerCase().includes(lowerCaseSearchTerm);
                    });
                }).map(terminal => {
                    // Create a new object for export to ensure correct date format
                    const exportTerminal = { ...terminal };
                    if (exportTerminal["CONFIGURE DATE"]) {
                        exportTerminal["CONFIGURE DATE"] = formatDateToDMonYY(exportTerminal["CONFIGURE DATE"]);
                    }
                    // Remove the internal 'status' and 'appVersion' properties if they are not part of newHeaders
                    delete exportTerminal.status;
                    delete exportTerminal.appVersion;
                    return exportTerminal;
                });

                // Ensure headers are in the correct order for the exported file
                const exportHeaders = newHeaders.filter(header => header !== "S/N"); // S/N is not a real data column

                const ws = XLSX.utils.json_to_sheet(dataToExport, { header: exportHeaders });
                const wb = XLSX.utils.book_new();
                XLSX.utils.book_append_sheet(wb, ws, "Live Terminals");
                XLSX.writeFile(wb, "Live_Terminals_Data.xlsx");
                showMessage('LIVE TERMINAL DATA DOWNLOADED SUCCESSFULLY!', 'success');
            });
        });

        // =====================================================================================================
        // Removed: All functions and global variables related to Configuration Generator
        // =====================================================================================================

        // Navigation Logic
        document.addEventListener('DOMContentLoaded', function() {
            const terminalDashboardSection = document.getElementById('terminalDashboard');
            const configGeneratorSection = document.getElementById('configGenerator'); // This will now be null or hidden
            const showDashboardLink = document.getElementById('showDashboard');
            // Removed: const showConfigGeneratorLink = document.getElementById('showConfigGenerator');
            const dropdownMenuButton = document.getElementById('dropdownMenuButton');
            const myDropdown = document.getElementById('myDropdown');

            function showSection(sectionId) {
                terminalDashboardSection.classList.add('hidden-section');
                // Ensure configGeneratorSection is handled gracefully if it no longer exists
                if (configGeneratorSection) {
                    configGeneratorSection.classList.add('hidden-section');
                }

                document.getElementById(sectionId).classList.remove('hidden-section');
            }

            showDashboardLink.addEventListener('click', (e) => {
                e.preventDefault();
                showSection('terminalDashboard');
                myDropdown.classList.remove('show-dropdown'); // Close dropdown after selection
            });

            // The link for configGenerator is removed from HTML, so this event listener is also effectively removed.
            // If it were still present, it would try to show a non-existent section.
            // showConfigGeneratorLink.addEventListener('click', (e) => {
            //     e.preventDefault();
            //     showSection('configGenerator');
            //     myDropdown.classList.remove('show-dropdown');
            // });

            // Toggle dropdown visibility on button click
            dropdownMenuButton.addEventListener('click', (e) => {
                e.stopPropagation(); // Prevent this click from bubbling up to the document and closing immediately
                myDropdown.classList.toggle('show-dropdown');
            });

            // Close the dropdown if the user clicks outside of it
            document.addEventListener('click', (e) => {
                if (!dropdownMenuButton.contains(e.target) && !myDropdown.contains(e.target)) {
                    myDropdown.classList.remove('show-dropdown');
                }
            });

            // Initially show the dashboard
            showSection('terminalDashboard');
        });
    </script>
</body>
</html>
