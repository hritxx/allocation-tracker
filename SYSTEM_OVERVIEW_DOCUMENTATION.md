# Employee Management System - Complete System Overview

## 🎯 System Purpose

This Employee Management System is designed to efficiently manage employees, projects, and task allocations while integrating with external HR systems like SumHR. It provides comprehensive project tracking, employee task management, and automated reporting capabilities.

---

## 👥 System Users

### 1. **Admin/HR Manager**

**Primary Responsibilities:**

- Overall system administration and employee management
- Project creation and allocation management
- Data imports from external systems (SumHR)
- Generate comprehensive reports and analytics

**What they can see and do:**

- **Employee Management**: View all employees, their profiles, skills, and status
- **Project Management**: Create projects, assign employees, set allocation percentages
- **Data Import**: Upload Employee Master and Daily Attendance reports from SumHR
- **Allocation Control**: Modify project allocations, update project status
- **Reporting**: Generate standard and custom HR reports
- **System Logs**: Monitor all system activities and user operations
- **Database Management**: Backup, restore, and manage historical data
- **Query Assistant**: Run custom SQL queries using natural language

### 2. **Manager/Project Lead**

**Primary Responsibilities:**

- Monitor assigned projects and team performance
- Track project progress and team contributions
- Request allocation changes when needed

**What they can see and do:**

- **Project Dashboard**: View all assigned projects and team members
- **Team Overview**: See employee allocations and their current assignments
- **Weekly Reports**: Access AI-generated weekly task summaries for team members
- **Performance Tracking**: Monitor project-wise employee contributions
- **Request Updates**: Communicate with HR for allocation changes
- **Task Analytics**: View detailed task breakdowns by employee and project

### 3. **Employee**

**Primary Responsibilities:**

- Submit daily tasks and time entries
- Maintain accurate project-wise work logs
- Update task progress regularly

**What they can see and do:**

- **Daily Task Entry**: Add tasks with project selection, description, and hours
- **Project Selection**: Choose from assigned projects via dropdown
- **Task History**: View and edit last 5 task entries
- **Time Tracking**: Log hours spent on specific projects
- **Personal Dashboard**: View own allocations and project assignments
- **Session Management**: 20-minute auto-timeout for security

### 4. **System Administrator (Sysadmin)**

**Technical Responsibilities:**

- System maintenance and monitoring
- Database administration and optimization
- Backup and recovery operations
- Performance tuning

---

## 🏢 Key Entities

### **Primary Entities:**

1. **Employee**

   - Personal details, contact information, employment data
   - Skills, designations, department assignments
   - Authentication credentials and session management

2. **Project**

   - Project details, status, timelines
   - Resource requirements and allocation tracking
   - Progress monitoring and reporting

3. **Department & Designation**

   - Organizational structure and hierarchy
   - Business unit classifications

4. **Daily Tasks**

   - Employee task entries with project mapping
   - Time tracking and progress updates
   - Weekly aggregation for reporting

5. **Project Allocations**

   - Employee-to-project assignments
   - Percentage-based allocation tracking
   - Historical allocation changes

6. **Attendance**
   - Daily attendance records from SumHR
   - Work duration and shift tracking

---

## 📊 Data Ownership & Sources

### **External Data Sources:**

1. **SumHR Integration**
   - **Employee Master Report**: Complete employee profile data (41 fields including personal, professional, and financial information)
   - **Daily Attendance Report**: Attendance records with in/out times, work duration, overtime tracking

### **Internal Data Generation:**

1. **Admin-Provided Data:**

   - Project definitions and requirements
   - Allocation assignments and modifications
   - Manual employee registrations
   - System configurations

2. **Manager-Provided Data:**

   - Performance feedback and ratings
   - Project status updates
   - Allocation change requests

3. **Employee-Provided Data:**
   - Daily task descriptions and hours
   - Project-wise work contributions
   - Time tracking entries

### **Data Flow:**

```
SumHR → CSV Reports → System Import → Internal Database
                ↓
Employee Tasks → Daily Entries → Weekly Aggregation → AI Reports
                ↓
System Analytics → Reports → Management Dashboards
```

---

## 🔄 Data Operations

### **Imports into the System:**

- **Employee Master CSV**: Automated parsing and employee creation/updates
- **Daily Attendance CSV**: Attendance tracking and work duration monitoring
- **Bulk Project Data**: CSV-based project and allocation imports
- **Skills Data**: Employee skills and competency mapping

### **Edits within the System:**

- **Real-time Task Entries**: Employees updating daily tasks
- **Allocation Modifications**: Admin adjusting project assignments
- **Project Status Updates**: Managers updating project progress
- **Employee Profile Updates**: HR maintaining employee information

### **Exports from the System:**

- **PDF Reports**: Employee profiles, project summaries, attendance reports
- **CSV Exports**: Data extracts for external analysis
- **Weekly Summaries**: AI-generated project and employee reports
- **Custom Query Results**: On-demand data analysis exports

---

## ⚙️ System Assumptions

1. **Email-based Authentication**: All users have valid email addresses for OTP verification
2. **SumHR Integration**: Regular data updates from SumHR system (Employee Master & Attendance)
3. **Project-based Work**: All employee tasks are tied to specific projects
4. **Daily Task Entry**: Employees will consistently log their daily activities
5. **Network Connectivity**: System requires internet access for email and AI features
6. **Data Consistency**: External data sources maintain consistent formats

---

## 🚀 Operational View

### **System Setup:**

1. **Infrastructure Deployment**: Docker-based containerized setup
2. **Database Initialization**: PostgreSQL with complete schema creation
3. **Sample Data Loading**: Seed data for initial system testing
4. **Email Configuration**: SMTP server setup for OTP delivery
5. **Redis Cache Setup**: Session management and OTP storage
6. **AI Service Integration**: Gemini API for automated reporting

### **System Initialization:**

1. **Database Creation**: Automated schema deployment
2. **Admin Account Setup**: Initial admin user creation
3. **Department Structure**: Organizational hierarchy setup
4. **Initial Data Import**: Employee Master and Attendance data loading
5. **Project Framework**: Basic project templates and categories

### **Daily Operations:**

- **Employee Task Logging**: Continuous task entry throughout the day
- **Attendance Sync**: Daily import of attendance data from SumHR
- **Session Management**: 20-minute timeout with Redis-based tracking
- **Real-time Analytics**: Live dashboard updates and reporting
- **System Monitoring**: Automated logging and error tracking

### **Weekly Operations:**

- **Automated Reports**: Cron-job scheduled weekly summary generation
- **Log Cleanup**: Automated removal of old system logs
- **Data Aggregation**: Weekly task summaries and project progress reports
- **Performance Analytics**: Employee and project performance metrics
- **Backup Validation**: Weekly backup integrity checks

---

## 🔐 Authentication Flow

### **Multi-Step Security Process:**

1. **Email Entry**: User enters registered email address
2. **OTP Generation**: System generates 6-digit verification code
3. **Email Delivery**: OTP sent via configured SMTP server
4. **Redis Storage**: OTP temporarily stored in Redis with expiration
5. **User Verification**: User enters received OTP
6. **Session Creation**: Valid OTP creates authenticated session
7. **Auto-Timeout**: Session expires after 20 minutes of inactivity
8. **Role-based Access**: Different UI/features based on user role

### **Security Features:**

- **No Password Storage**: Passwordless authentication system
- **Time-limited OTPs**: Codes expire after 5 minutes
- **Session Management**: Redis-based session tracking
- **Role-based Authorization**: Different access levels per user type
- **Activity Logging**: Complete audit trail of user actions

---

## 💻 Technology Stack

### **Frontend Technology:**

- **Streamlit**: Python-based reactive web framework
- **Plotly**: Interactive data visualization and charts
- **Responsive Design**: Mobile-friendly interface

### **Backend Technology:**

- **Python**: Core application language
- **SQLAlchemy**: Database ORM and query management
- **PostgreSQL**: Primary database for production
- **SQLite**: Development and testing database

### **Cache & Session Management:**

- **Redis**: Session storage and OTP management
- **In-memory Caching**: Fast data retrieval

### **Integration & AI:**

- **Google Gemini API**: AI-powered task summarization
- **SMTP Integration**: Email delivery system
- **CSV Processing**: Pandas for data import/export

### **Infrastructure:**

- **Docker**: Containerized deployment
- **Docker Compose**: Multi-service orchestration
- **Automated Backups**: Scheduled data protection

---

## ⏰ Cron Job Scheduler - Weekly Reports

### **Automated Weekly Summary Generation:**

**Schedule**: Every Monday at 9:00 AM

```bash
# Crontab entry
0 9 * * 1 /path/to/employee_management/run_weekly_summaries.sh
```

**Process Flow:**

1. **Data Collection**: Gather all tasks from previous week
2. **Employee Grouping**: Organize tasks by employee and project
3. **AI Processing**: Generate intelligent summaries using Gemini API
4. **Report Creation**: Create comprehensive weekly reports
5. **Manager Notification**: Distribute reports to relevant managers
6. **Storage**: Archive reports for historical reference

**Generated Reports Include:**

- **Employee Weekly Summary**: Individual task contributions and time allocation
- **Project Progress Reports**: Overall project advancement and team performance
- **Manager Dashboard Updates**: Team performance metrics and insights
- **Performance Analytics**: Under/over-performance identification
- **Resource Utilization**: Allocation efficiency and optimization suggestions

---

## 🎯 Efficiency Benefits

### **Employee Management Efficiency:**

- **Centralized Data**: Single source of truth for all employee information
- **Automated Imports**: Direct integration with SumHR reduces manual entry
- **Real-time Updates**: Instant reflection of changes across the system
- **Skills Tracking**: Comprehensive competency mapping and development tracking

### **Project Management Efficiency:**

- **Resource Optimization**: Data-driven allocation decisions
- **Progress Tracking**: Real-time project status and milestone monitoring
- **Performance Analytics**: Identify bottlenecks and optimization opportunities
- **Automated Reporting**: Reduce manual reporting overhead

### **Time Management Efficiency:**

- **Daily Task Tracking**: Granular time allocation and project contribution
- **Automated Summaries**: AI-generated weekly reports save management time
- **Historical Analysis**: Trend identification and future planning
- **Performance Insights**: Data-driven employee development decisions

### **Operational Efficiency:**

- **Passwordless Authentication**: Simplified but secure access
- **Session Management**: Automatic security with user convenience
- **Backup Automation**: Reliable data protection without manual intervention
