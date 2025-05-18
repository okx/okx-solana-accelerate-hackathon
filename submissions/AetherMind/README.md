
# AetherMind - Intelligent DeFi Navigator

## Project Introduction

AetherMind is an intelligent DeFi (Decentralized Finance) navigator designed to empower users to explore, simulate, and understand complex DeFi strategies. It leverages the power of AI (Google's Gemini models via Genkit) to provide personalized strategy suggestions and detailed explanations, grounded in real-time market data from OKX DEX. The platform connects to the user's Metamask wallet to offer insights relevant to their holdings.

**Core Goal:** To demystify DeFi by providing users with tools to simulate strategies, understand risks, and make more informed decisions in the dynamic world of decentralized finance, with a focus on the OKX DEX ecosystem.

## How it Works (Overall Flow)

1.  **Wallet Connection**: The user connects their Metamask wallet.
2.  **Wallet Overview**: A summary of the connected wallet is displayed, primarily showing the native currency balance (e.g., ETH). Full ERC20 token discovery and comprehensive valuation are planned future enhancements.
3.  **Risk Profile Selection**: Users can select a risk profile (Conservative, Balanced, Aggressive) to tailor AI suggestions.
4.  **AI-Powered Simulations**:
    *   **General Strategy Suggestions**: Users can request AI-generated DeFi strategy suggestions based on their native token holdings, selected risk profile, and current market conditions (sourced from OKX DEX).
    *   **Specific Strategy Simulation**: Users can choose predefined DeFi strategies (e.g., Yield Farming, Flash Loan Arbitrage), input specific parameters, and run a simulation. The AI provides a detailed explanation of the chosen strategy, potential outcomes (currently illustrative for profit/loss figures), and associated risks, contextualized by OKX DEX data.
5.  **Educational Insights**: The platform offers explanations for various DeFi strategies and common risks.
6.  **Recent Simulations**: A history of the user's recent simulations is stored locally (in-browser) and displayed for review.

## Key Features Explained

*   **Wallet Connection & Overview**:
    *   Integrates with Metamask (`window.ethereum`) for secure wallet connection.
    *   Displays the connected account address, network name, and native currency balance.
    *   Includes a "Copy Address" button and a "Refresh Balance" feature.
    *   **Files**: `src/hooks/useWallet.ts`, `src/components/aethermind/WalletConnect.tsx`, `src/components/aethermind/WalletOverview.tsx`.

*   **AI-Powered DeFi Simulator**:
    *   **Customizable Risk Profiles**: Allows users to select 'Conservative', 'Balanced', or 'Aggressive' risk profiles, which influences the strategies suggested by the AI.
        *   **UI**: `src/components/aethermind/SimulationArea.tsx`.
        *   **AI Logic**: `src/ai/flows/personalized-strategy-suggestions.ts`.
    *   **Specific Strategy Simulation**: Users can simulate:
        *   Yield Farming
        *   Flash Loan Arbitrage (conceptual, as true arbitrage simulation is complex)
        *   Users input parameters like asset, amount, and duration.
        *   The AI provides detailed explanations, potential outcomes (profit/loss figures are illustrative), and risks.
        *   **UI**: `src/components/aethermind/SimulationArea.tsx` (also contains strategy definitions).
        *   **AI Explanation Logic**: `src/ai/flows/defi-strategy-explanation.ts`.
    *   **General AI Strategy Suggestions**: The AI generates 3-5 personalized DeFi strategy suggestions based on user's native token holdings, real-time OKX DEX market conditions, and selected risk profile.
        *   **AI Logic**: `src/ai/flows/personalized-strategy-suggestions.ts`.

*   **Educational Insights**:
    *   **DeFi Strategy Info**: Cards for common strategies (e.g., Yield Farming, Flash Loans) with an option to "Learn More with AI," which fetches a detailed explanation.
        *   **UI**: `src/components/aethermind/DeFiStrategyInfo.tsx`.
        *   **AI Logic**: `src/ai/flows/defi-strategy-explanation.ts`.
    *   **Risk Information**: Static cards explaining common DeFi risks like Impermanent Loss, Smart Contract Risk, and Liquidation Risk.
        *   **UI**: `src/components/aethermind/AetherMindClientPage.tsx`.

*   **Recent Simulations Display**:
    *   Lists the user's recent simulations with key inputs and AI-generated results.
    *   Data is stored in `localStorage` to persist across page refreshes for the current browser session.
    *   **UI**: `src/components/aethermind/AetherMindClientPage.tsx`.

*   **Trending DeFi News (Mock)**:
    *   A card in the Wallet Overview displays mock trending news items to showcase potential future integration.
    *   **UI**: `src/components/aethermind/TrendingDeFiNewsCard.tsx`.

## OKX DEX API Integration

AetherMind integrates with the OKX DEX API v5 to fetch real-time market data, which is used to provide context for AI-powered simulations and strategy suggestions.

*   **Core Integration File**: `src/services/okxService.ts`
    *   This service module is responsible for all direct communication with the OKX API.
    *   **Authentication**:
        *   It implements the required HMAC-SHA256 signature generation for API requests using Node.js's built-in `crypto` module.
        *   The `getOkxAuthHeaders()` function constructs the necessary authentication headers (`OK-ACCESS-KEY`, `OK-ACCESS-SIGN`, `OK-ACCESS-TIMESTAMP`, `OK-ACCESS-PASSPHRASE`).
        *   API credentials (Key, Secret, Passphrase) are securely read from environment variables defined in the `.env` file.
    *   **Data Fetching Functions**:
        *   `fetchOkxMarketSummary()`:
            *   Makes GET requests to the `/api/v5/market/ticker` OKX endpoint.
            *   Fetches current ticker data (last price, 24h volume, 24h change) for key trading pairs: `BTC-USDT`, `ETH-USDT`, and `OKT-USDT`.
            *   Constructs a string summary of these market conditions.
        *   `fetchTokenPriceFromOKX(tokenSymbol: string)`:
            *   Designed to fetch the current USD price for a given token symbol by querying its `-USDT` pair (e.g., `ETH-USDT`) from the `/api/v5/market/ticker` endpoint.
            *   This function is available but not yet fully integrated into the real-time valuation of all tokens in the user's wallet overview.

*   **How OKX DEX Data is Used in the Project**:
    *   The market summary string generated by `fetchOkxMarketSummary()` is retrieved by the `getOkxMarketConditions()` server action in `src/lib/actions.ts`.
    *   This market condition data is then passed as input to the Genkit AI flows:
        *   `src/ai/flows/personalized-strategy-suggestions.ts`: Uses market conditions to tailor DeFi strategy advice.
        *   `src/ai/flows/defi-strategy-explanation.ts`: Uses market conditions to provide relevant context when explaining specific DeFi strategies (e.g., how current volatility might affect a yield farming strategy on OKX DEX).
    *   This ensures that AI-generated insights are more relevant and grounded in actual, albeit selectively fetched, market data from OKX DEX.

*   **Current Status of Integration**:
    *   The `okxService.ts` is implemented to make live API calls for fetching market summaries for the specified pairs.
    *   API key handling and request signing are in place.
    *   Error handling for API requests is included.

## AI Integration (Genkit & Gemini)

AetherMind utilizes Genkit, an open-source framework, to integrate with Google's Gemini AI models for its intelligent features.

*   **Core AI Files**:
    *   `src/ai/genkit.ts`: Configures and initializes the Genkit instance, specifying the use of `googleAI()` plugin (for Gemini models). It sets a default model (e.g., `gemini-2.0-flash`).
    *   `src/ai/flows/defi-strategy-explanation.ts`:
        *   A Genkit flow that defines an AI prompt to explain a given DeFi strategy in detail.
        *   Input: Strategy name and parameters.
        *   Output: A structured HTML explanation covering mechanics, potential risks (e.g., impermanent loss, smart contract vulnerabilities), considerations for OKX DEX, and advice on what to research before proceeding.
    *   `src/ai/flows/personalized-strategy-suggestions.ts`:
        *   A Genkit flow that defines an AI prompt to generate personalized DeFi strategy suggestions.
        *   Input: User's token holdings (currently native balance), OKX DEX market conditions (from `okxService.ts`), and user's selected risk profile.
        *   Output: A list of 3-5 suggested DeFi strategies suitable for the user on OKX DEX, formatted as HTML, along with a rationale explaining the choices.

*   **How AI is Used**:
    *   Server actions in `src/lib/actions.ts` (`getStrategyExplanation`, `getPersonalizedSuggestions`) act as wrappers around these Genkit flows, making them callable from client components.
    *   `DeFiStrategyInfo.tsx` calls `getStrategyExplanation` when a user wants to learn more about a general strategy.
    *   `SimulationArea.tsx` calls `getPersonalizedSuggestions` to get tailored advice and also uses `getStrategyExplanation` when a user simulates a specific strategy to provide a detailed breakdown.
    *   The AI responses are requested in HTML format to ensure proper rendering in the UI.

## Tech Stack

*   **Frontend**: Next.js (App Router), React, TypeScript
*   **Styling**: Tailwind CSS, ShadCN UI components
*   **AI**: Genkit, Google Gemini Models
*   **Icons**: Lucide React
*   **Wallet Interaction**: Ethers.js (via `window.ethereum` for Metamask)
*   **API Interaction**: Native `fetch` for OKX DEX API, Node.js `crypto` for request signing.

## How to Run Your Project

1.  **Clone the Repository**:
    ```bash
    git clone <your-repository-url>
    cd aethermind-project-directory
    ```

2.  **Install Dependencies**:
    ```bash
    npm install
    # or
    yarn install
    ```

3.  **Set Up Environment Variables**:
    *   Create a `.env` file in the root directory of the project.
    *   Add your API keys to this file:
        ```plaintext
        # For Google Gemini AI
        GEMINI_API_KEY=YOUR_GEMINI_API_KEY

        # For OKX DEX API
        OKX_API_KEY=YOUR_OKX_API_KEY_FROM_OKX_DASHBOARD
        OKX_SECRET_KEY=YOUR_OKX_SECRET_KEY_FROM_OKX_DASHBOARD
        OKX_PASSPHRASE=YOUR_OKX_API_PASSPHRASE_FROM_OKX_DASHBOARD
        ```
    *   Ensure the OKX API key has "Read" permissions.

4.  **Run the Development Server**:
    The project uses a combined script to run both the Next.js app and the Genkit development server.
    ```bash
    npm run dev
    ```
    This typically starts:
    *   Next.js application on `http://localhost:9002` (or the port specified in your `package.json`).
    *   Genkit development server (check console output, often `http://localhost:4000` or `http://localhost:3400` for the Genkit Inspector).

5.  **Open in Browser**:
    Navigate to `http://localhost:9002` (or your Next.js app's port) in your web browser.

## Additional Information

*   **Current Limitations**:
    *   **Wallet Overview**: Primarily displays native currency balance. Full ERC20 token discovery and real-time USD valuation for all assets are not yet implemented.
    *   **OKX DEX Data**: While `fetchOkxMarketSummary` provides live data for selected pairs, other parts of the simulation (like potential profit/loss figures for specific strategies) are still illustrative and use mock calculations rather than deep, real-time simulation against OKX DEX order books or liquidity pools.
    *   **Flash Loan Arbitrage Simulation**: This is highly conceptual. Simulating true flash loan arbitrage profitability requires complex, high-frequency data and execution logic beyond the current scope.
    *   **Error Handling**: Basic error handling is in place, but can be further enhanced for a production environment.
*   **Security**: API keys are intended to be kept secure in the `.env` file and used server-side. No private keys are handled by the application. All transactions requiring wallet interaction (if implemented for execution) would go through Metamask for user approval.
*   **Future Enhancements**:
    *   Full ERC20 token discovery and valuation in Wallet Overview.
    *   Deeper integration with OKX DEX for more realistic simulation of trade execution, liquidity provision, and yield farming outcomes.
    *   Implementation of other features from the roadmap (Backtesting, Automated Strategy Execution (with caution), IL Prediction, Social Sharing, Portfolio Forecaster, DeFi Academy).
    *   More sophisticated state management for recent simulations (e.g., persistent storage beyond `localStorage` if needed).
    *   Enhanced UI/UX for data visualization (e.g., charts for portfolio breakdown).

## Screenshots:

![Screenshot (1215)](https://github.com/user-attachments/assets/e04942ff-f708-4e9c-9e31-a8308b58d6d8)

![Screenshot (1218)](https://github.com/user-attachments/assets/ef4ba9fc-8e4c-4d0e-94f6-d268577612dd)

![Screenshot (1219)](https://github.com/user-attachments/assets/c06a4384-dbca-4901-8b0a-6a6f907dd528)

![Screenshot (1220)](https://github.com/user-attachments/assets/85e92d2f-5f9c-4a24-bff4-9e1fbcb3e369)

![Screenshot (1223)](https://github.com/user-attachments/assets/83354072-0d61-4552-a48e-f0206b743efb)

![Screenshot (1224)](https://github.com/user-attachments/assets/9576ea2a-18d6-485d-9432-57b515e6f14a)

![Screenshot (1225)](https://github.com/user-attachments/assets/ef111bfa-e9c6-476e-b0b1-7d4e6b24357d)

![Screenshot (1226)](https://github.com/user-attachments/assets/eb39bd43-b4dd-4eee-a950-9517f5ad79a8)








