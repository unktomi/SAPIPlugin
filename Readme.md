This plugin requires the Windows 7+ SDK.

Provides and actor <code>SAPI Actor</code> which receives speech recognition events

    void OnSpeechInputStarted();

    void OnSpeechInputStopped();
 
    void OnSpeechRecognized(const FString &SpeechText); // JSON formatted SRGS output
 
    void OnSpeechRecognitionError(const FString &ErrorMessage, 
                                  const FString &Source, 
                                  int32 LineNumber, 
                                  const FString &ScriptLine);

Also provides a modal latent action which waits for a response from the user that matches the current grammar:  

    void GetResponse(FString &ResponseText) // JSON formatted SRGS output


Provides the following library functions to manage the recognizer including SRGS grammars

Text to speech

    void Speak(const FString &SpeechText);
    
Set language (En_US or En_UK)

    void SetLanguage(ELanguage Language);
    
Pause the recognizer

    void PauseSpeechRecognition();

Resume the recognizer

    void ResumeSpeechRecognition();

Enable or disable the specified grammar (file must be relative to the root of your Game directory)

    void SetGrammar(const FString &GrammarFile, bool Enabled);

Enable or disable the specified grammar rule, e.g "Grammars/MyGrammar.grxml#Rule1"

    SetRule(const FString &RuleUrl, bool Enabled);
    
Used in conjunction with GetResponse. Temporarily disables current grammars and enables the specified grammar

    void PushGrammar(const FString &GrammarFile);

Used in conjunction with GetResponse. Enables grammars in effect before the last PushGrammar
    
    void PopGrammar();

Dynamically modifiy the specified grammar rule

    void AddWordTransition(const FString &RuleUrl, 
                           const TArray<FString> &Words, 
                           bool Overwrite = false, 
                           const FString &WordSeparator = TEXT(";"));

Manually send audio to the recognizer

    void SendAudio(const TArray<uint8> &Samples, int32 Channels, int32 SamplesPerSecond);


