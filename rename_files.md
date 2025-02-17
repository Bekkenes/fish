# Rename Files in Fish Shell

A Fish shell function to **mass rename files** by removing leading numbers, dots, and spaces from filenames.

## Features

✅ Supports any file extension.
✅ Removes **leading numbers, dots, and spaces** while keeping the rest of the filename intact.
✅ **Dry-run mode** to preview changes before renaming.
✅ Safe and efficient bulk renaming.

---

## Installation

1. Copy and paste the function into your Fish shell:

   ```fish
   function rename_files
       if test (count $argv) -lt 1 -o (count $argv) -gt 2
           echo "Usage: rename_files <extension> [--dry-run]"
           return 1
       end

       set ext $argv[1]
       set dry_run 0

       if test (count $argv) -eq 2
           if test "$argv[2]" = "--dry-run"
               set dry_run 1
           else
               echo "Invalid option: $argv[2]"
               return 1
           end
       end

       for file in *.$ext
           set new_name (string replace -r '^\d+\.\s*' '' -- "$file")

           if test "$file" != "$new_name"
               if test $dry_run -eq 1
                   echo "Would rename: '$file' -> '$new_name'"
               else
                   mv "$file" "$new_name"
                   echo "Renamed: '$file' -> '$new_name'"
               end
           end
       end
   end
   ```

2. Save the function permanently so Fish remembers it:

   ```fish
   funcsave rename_files
   ```

---

## Usage

### Rename Files Normally

To rename all files with a specific extension:

```fish
rename_files nes
```

#### Example:

**Before:**

```
01. Super Mario Bros. 3 (USA).nes
02. The Legend of Zelda (USA).nes
03. Metroid (USA).nes
```

**After:**

```
Super Mario Bros. 3 (USA).nes
The Legend of Zelda (USA).nes
Metroid (USA).nes
```

### Dry-Run Mode (Preview Before Renaming)

To see what changes will be made **without renaming**:

```fish
rename_files nes --dry-run
```

#### Example Output:

```
Would rename: '01. Super Mario Bros. 3 (USA).nes' -> 'Super Mario Bros. 3 (USA).nes'
Would rename: '02. The Legend of Zelda (USA).nes' -> 'The Legend of Zelda (USA).nes'
Would rename: '03. Metroid (USA).nes' -> 'Metroid (USA).nes'
```

---

## Notes

- Works with any file extension (replace `nes` with any other extension like `txt`, `mp3`, etc.).
- Does **not** rename files that don’t start with numbers.
- Safe to use since dry-run mode allows previewing changes before renaming.

---

## License

MIT License

README.md
