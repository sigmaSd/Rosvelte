# Rosvelte
Simple radio interface using svelte

## Usage
- `npm run dev`

You can also use a script for easier usage (fish example):
```fish
function radio
  cd $repoPath/public/
  python -m http.server&
  firefox http://localhost:8000/
  fg
end
```

