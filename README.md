# LiftUp - Social Protection & Livelihoods Platform
## Vision: A World Without Poverty


LiftUp is a sophisticated desktop application designed to combat poverty by creating a digital ecosystem for social protection and economic empowerment. Our mission is to provide a powerful yet user-friendly tool for non-profits, government agencies, and community leaders to connect vulnerable individuals with life-changing opportunities.

This application serves as a demonstration of how technology can be harnessed to:
- **Organize and manage** data for beneficiaries and opportunities.
- **Intelligently match** individuals to jobs or training based on their skills.
- **Visualize impact** through a comprehensive data dashboard.
- **Simulate support** to demonstrate pathways for financial inclusion.

## Features

- **Beneficiary Management**: Add, edit, and manage a list of beneficiaries, including their household size and skills.
- **Opportunity Management**: Maintain a list of available jobs, training programs, or other opportunities with required skills and payout details.
- **Intelligent Matching**: A powerful matching engine that connects beneficiaries to suitable opportunities based on skill overlap.
- **Simulated Wallet**: A demo feature to simulate direct financial support to beneficiaries, showcasing a vision for secure and transparent aid distribution.
- **Advanced Dashboard**: An interactive dashboard with Key Performance Indicators (KPIs) and charts to visualize data, including:
  - Total Beneficiaries & Opportunities
  - Average Household Size
  - Total Opportunity Value
  - Top In-Demand Skills
  - Highest Payout Opportunities
- **User-Friendly Interface**:
  - Intuitive layout with clear icons and tooltips.
  - Light and Dark mode themes.
  - Adjustable font size for accessibility.
  - Persistent settings for theme and font size.
- **Data Portability**: Export beneficiary and opportunity data to CSV files.
- **Sample Data**: Load sample data to quickly explore the application's features.

## Finish-Up-A-Thon Revival

LiftUp already had a working core, but it lacked finish quality. This revival pass focused on reliability and continuity: persistent preferences, deterministic save behavior on app exit, and a cleaner, more stable user flow.

Before this pass, the project behaved like an academic prototype. After the refresh, it behaves like a production-minded desktop tool with stronger data continuity and a clearer completion arc.

GitHub Copilot accelerated the transition by helping tighten lifecycle handling, persistence flow, and UI wiring so the project could be presented as a finished product rather than a rough demo.

## How to Run

For the full challenge write-up and technical evidence, see:

[FINISH_UP_A_THON_SUBMISSION.md](FINISH_UP_A_THON_SUBMISSION.md)

This project is built with Java 17 and JavaFX, using Maven for dependency management.

### Prerequisites
- **Java Development Kit (JDK)**: Version 17 or higher.
- **Apache Maven**: Version 3.6 or higher.

### Steps to Run
1. **Clone the repository or download the source code.**
2. **Open a terminal or command prompt** and navigate to the project's root directory (where `pom.xml` is located).
3. **Compile and run the application** using one of the following Maven commands:
   ```shell
   mvn clean compile exec:java -Dexec.mainClass="com.liftup.Launcher"
   ```
  or
  ```shell
  mvn javafx:run
  ```
4. The application window will launch.

## Data Persistence

LiftUp stores local data in the user home directory under `.liftup/`:

- `data.json`: Beneficiaries and opportunities.
- `prefs.json`: Theme and font-scale preferences.

The Save button triggers data serialization immediately, and app shutdown also persists state through the JavaFX lifecycle hook.

## How to Deploy

1.  **Package the application** into a JAR file using the following command:
    ```shell
    mvn clean package
    ```
2.  **Create a native installer** for your operating system:
    ```shell
    mvn jpackage:jpackage
    ```
    The installer will be created in the `target/dist` directory.

## Technologies Used

- **Language**: Java 17
- **Framework**: JavaFX 21 (for the user interface)
- **Build Tool**: Apache Maven
- **Libraries**:
  - **Gson**: For saving and loading data from JSON files.

---

LiftUp demonstrates how a JavaFX desktop workflow can support social-impact operations with practical data handling, transparent matching logic, and continuity-focused user experience.