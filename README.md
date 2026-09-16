# Add these tickers to whatever list/dict drives the price fetch
# Listed equities — Yahoo Finance will return data
ADDITIONAL_TICKERS = {
    # Hyperscalers
    "GOOGL": "Alphabet Inc.",
    "AMZN": "Amazon.com Inc.",
    "META": "Meta Platforms Inc.",
    "IBM": "IBM Corporation",

    # Semiconductors / AI hardware
    "AVGO": "Broadcom Inc.",
    "QCOM": "Qualcomm Inc.",
    "ARM":  "ARM Holdings plc",
    "MU":   "Micron Technology Inc.",
    "AMAT": "Applied Materials Inc.",
    "INTC": "Intel Corporation",

    # Memory
    "005930.KS": "Samsung Electronics Co., Ltd.",

    # Financial investors (publicly listed)
    "BX":   "Blackstone Inc.",
    "CG":   "Carlyle Group Inc.",
    "JPM":  "JPMorgan Chase & Co.",
    "C":    "Citigroup Inc.",
    "GS":   "The Goldman Sachs Group Inc.",
    "MS":   "Morgan Stanley",

    # Competing infrastructure / HPC
    "CORZ": "Core Scientific Inc.",

    # Defence / industrial (in AI theme)
    "RTX":  "RTX Corporation",
    "LMT":  "Lockheed Martin Corporation",
    "NOC":  "Northrop Grumman Corporation",
    "GD":   "General Dynamics Corporation",
    "BA":   "The Boeing Company",

    # Energy (in AI power theme)
    "XOM":  "ExxonMobil Corporation",
    "SHEL": "Shell plc",
    "BP":   "BP p.l.c.",
    "CVX":  "Chevron Corporation",

    # Materials (critical minerals)
    "RIO":  "Rio Tinto plc",
    "FCX":  "Freeport-McMoRan Inc.",

    # Shipping / logistics
    "MAERSK-B.CO": "A.P. Møller-Maersk A/S",

    # Already have but verify coverage
    "NVDA": "NVIDIA Corporation",
    "TSM":  "Taiwan Semiconductor Manufacturing Co.",
    "ASML": "ASML Holding N.V.",
    "AMD":  "Advanced Micro Devices Inc.",
    "INTC": "Intel Corporation",
    "SKHY": "SK Hynix Inc.",
    "MSFT": "Microsoft Corporation",
    "AAPL": "Apple Inc.",
}

# These are private — explicitly mark, do not attempt to fetch
PRIVATE_NO_PRICE_HISTORY = {
    "COREWEAVE":  "CoreWeave Inc.",
    "ANTHROPIC":  "Anthropic PBC",
    "OPENAI":     "OpenAI",
    "MISTRAL":    "Mistral AI",
    "LAMBDA":     "Lambda Inc.",
    "REPLICATE":  "Replicate",
    "CHAI":       "Chai Discovery",
}
