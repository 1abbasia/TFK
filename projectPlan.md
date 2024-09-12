## Component Breakdown

### 1. Frontend (React Application)

#### a. Home Page (src/pages/Home.js)
- Main landing page
- Displays truck status and location
- Shows a summary of the menu
- Links to full menu and catering form

#### b. Menu Section (src/components/Menu.js)
- Fetches and displays all menu items
- Grouped by categories (if applicable)

#### c. Location Status (src/components/LocationStatus.js)
- Displays current truck status (OPEN/CLOSED)
- Shows current location when open
- Uses real-time subscription to update instantly

#### d. Catering Form (src/components/CateringForm.js)
- Form for customers to submit catering requests
- Sends data to Supabase on submission

#### e. Admin Page (src/pages/Admin.js)
- Protected route for truck owner
- Allows updating truck status and location

#### f. Supabase Client (src/utils/supabaseClient.js)
- Initializes and exports Supabase client for use in components

### 2. Backend (Supabase)

#### a. PostgreSQL Database
- truck_status table:
id: int (primary key)
status: string
location: string
updated_at: timestamp

- menu_items table:
id: int (primary key)
name: string
description: string
price: decimal
category: string (optional)

- catering_requests table:
  id: int (primary key)
name: string
email: string
event_date: date
number_of_guests: int
message: text
created_at: timestamp

#### b. Authentication
- Handles admin login for the truck owner
- Secures the admin page and status update functionality

#### c. Realtime Engine
- Enables real-time updates for truck status changes

### 3. Hosting
- Static hosting service (e.g., Netlify, Vercel)
- Serves the React app to users' browsers

## Data Flow

1. Initial Load:
 - React app loads in the browser
 - Fetches initial data (menu items, truck status) from Supabase
 - Sets up real-time subscription for truck status updates

2. Truck Status Update:
 - Admin updates status via admin page
 - Update sent to Supabase
 - Realtime Engine broadcasts change
 - All connected clients receive update and refresh their UI

3. Catering Request:
 - User fills out catering form
 - Form data sent to Supabase on submission
 - Stored in catering_requests table

4. Menu Display:
 - Menu items fetched from Supabase on component mount
 - Displayed in Menu component