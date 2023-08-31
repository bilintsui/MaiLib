# MaiLib

## A library for processing maimai charts

> One example implementation is MaichartConverter, which converts between Simai and Ma2. Please
> see [MaichartConverter](https://github.com/Neskol/MaichartConverter) for more information.

### Build

    git clone
    dotnet build

### Usage

- The most basic part of this is `Chart` - you can use this to construct different charts.
- This library follows the Tokenizer-Parser-Compiler format to process files, and uses an Abstract Syntax Tree for grammar
  decomposition when implementing Simai and Ma2 formats. If you wish to add additional formats, please make sure you
  also process files in the same fashion as this library, and ensure that all methods within the `ITokenizer`, `IParser`,
  and `ICompiler` interfaces are properly implemented.
- The `Chart` base class is an intermediary in order to achieve inter-format compatability. If you are adding a new format,
  please be sure to also create a class implementing this base class. The `Chart` class has already implemented the functions
  you need for a maimai chart, and you only need to implement several abstract methods in that class to fit your
  format.
- Then, you may create a maimai chart instance in your code. For example, creating a Ma2 chart can be done
  via `Chart ma2Chart = new Ma2();`.

## Additional notice for Simai compatability

- As always, I think Simai is a language more focusing on charting rather than interpreting. I still have no idea why
  there isn't a UI-based charting tool, instead we have to learn this unsecure and unintuitive language, especially after
  Festival added new features. This makes interpreting Simai a huge PAIN since the way it converts between ticks and
  times is vague and honestly unreasonable.
- For example, it defines a Slide note as having a wait time of 1 beat or one 1/4 note (or a crotchet for those in the music community)
  after its start tap. If your Slide note starts longer or shorter than 1 quaver of current BPM, you will have to: a) change
  the BPM for that specific Slide or b) define the time by [wait time##last time] - and calculating that is extremely
  time consuming.
- I hope someone develops a language better than Simai to use as a intermediate language between coding and charting.
  Thank you.

### Parameters notice

- music files should be named `musicxxxxxx.mp3`, where 'xxxxxx' matches the music ID specified in `music.xml` in each a000
  folder. Please make sure to add 0s at the front of this so that it contains 6 digits
- bga files should be named `xxxxxx.mp4` which matches the music ID specified in `music.xml` in each a000 folder. Please make sure to add 0s at the front of this so that it contains 6 digits
- image folders should be structured in `image/Texture2D/` and the files should start with 'UI_Jacket_xxxxxx.jpg', where
  'xxxxxx' matches the music id specified in `music.xml` in each a000 folder. Please make sure to add 0s at the front of this so that it contains 6 digits
- The difficulty parameter is listed 0-4, from Basic to Re:Master. In MaiLib, I specified rules for Easy and Utage but it
  takes time for me to figure it out, or you could implement it on your own, referring MaiLib code
- All paths, reguardless of operating system, should end with a path separator like "/" or "\". Do not include the quotation marks in the path.
- If you have difficulty using the commands, please refer to `VSCode launch.json` where I included several examples.
- The whole program was initially planned to convert from ma2 to simai, and all other features were developed after that,
  so there is a HUGE amount of compromises in code design which makes it hard to read (but works so far). It would be
  most kind of you if you would like to help me in fixing that.

### Disclaimer

- Copyright of all works within this repository belongs to their respective rights holders. This tool is made solely for personal use. Please use any resources not found within this repository at your own risk.
- If you would like to use this parser in your project, please refer to [MaiLib](https://github.com/Neskol/MaiLib) and
  hopefully that helps!
