# A/B Testing Vue 3 Implementation

Simple Vue 3 implementation for A/B testing that assigns users to groups based on their UUID.

## Quick Start

1. **Install dependencies**
```bash
npm install
# or 
yarn install
```

2. **Run the project**
```bash
npm run dev
# or
yarn dev
```

## How It Works

- Stores UUID in localStorage (generates on first visit)
- Assigns users to groups based on UUID's last character:
  - A-J → Group A
  - K-Z, 0-9 → Group B
- Displays a button showing user's group assignment

## Features

- Persistent user identification across sessions
- Simple and lightweight implementation
- Easy to extend for multiple test variations
- No external A/B testing service required

## Dependencies

- Vue 3
- uuid

## Future Improvements

- Add analytics tracking
- Implement more sophisticated group assignment algorithms
- Create multiple concurrent experiments