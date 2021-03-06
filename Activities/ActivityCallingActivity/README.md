### Code Snippets

> MainActivity.java

```java
        launchButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent startSecondActivityIntent = new Intent(MainActivity.this, SecondActivity.class);
                startSecondActivityIntent.putExtra(SecondActivity.EXTRA_MESSAGE, R.string.message1);
                startSecondActivityIntent.putExtra(SecondActivity.INFORM_MESSAGE, R.string.inform_message);

                startActivity(startSecondActivityIntent);

                Log.d(TAG, "startActivity() is a is an ASYNCHRONOUS call");
            }
        });

        launchButtonForResult.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent startSecondActivityForResultIntent = new Intent(MainActivity.this, SecondActivity.class);

                startSecondActivityForResultIntent.putExtra(SecondActivity.EXTRA_MESSAGE, R.string.message2);
                startSecondActivityForResultIntent.putExtra(SecondActivity.INFORM_MESSAGE, R.string.inform_message);

                startActivityForResult(startSecondActivityForResultIntent, 0);

                Log.d(TAG, "startActivityForResult() is an ASYNCHRONOUS call");
            }
        });
        
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);

        if(data == null) {
            return;
        }

        switch(requestCode) {
            case 0:
                int message = data.getIntExtra(SecondActivity.RESULT, -1);
                Toast.makeText(getApplicationContext(), String.valueOf(message), Toast.LENGTH_SHORT).show();
        }
    }        
```

> SecondActivity.java

```java
    public static final String EXTRA_MESSAGE = "com.lifecycle.activity.droid.activitycallingactivity.message";
    public static final String INFORM_MESSAGE = "com.lifecycle.activity.droid.activitycallingactivity.inform";

    public static final String RESULT = "com.lifecycle.activity.droid.activitycallingactivity.result";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);

        int message1ResourceId = getIntent().getIntExtra(EXTRA_MESSAGE, -1);
        int message2ResourceId = getIntent().getIntExtra(INFORM_MESSAGE, -1);

        String message1 = getResources().getString(message1ResourceId);
        String message2 = getResources().getString(message2ResourceId);

        Toast.makeText(getApplicationContext(), message1 + "\n" + message2, Toast.LENGTH_LONG).show();

        Button closeButton = (Button)findViewById(R.id.close_button);

        closeButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                SecondActivity.this.finish();
            }
        });

        Button returnResultButton = (Button)findViewById(R.id.return_result_button);

        returnResultButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent result = new Intent();

                result.putExtra(RESULT, 10);

                setResult(RESULT_OK, result);
            }
        });
    }
```

### Flow Diagram

<img src="https://github.com/gruprog/Android-Examples/blob/master/Activities/ActivityCallingActivity/_misc/block%20diagram.png"/>
