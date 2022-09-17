
<!-- # ![mg-builder](/img~/mg-builder.png) -->

# Lesson 2

Developing Mobile Game lesson for Ankara university - Week 2

At the beginning of the lesson , "Package Manager" will be mentioned.
Then we will import Dotween and CartoonFX unitypackages from asset store.

## Demo 1 

* Scene Works
* Motion
* FixedUpdate

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo1.png"></td>

  </tr>
 </table>

 ```csharp

using UnityEngine;

public class Player : MonoBehaviour
{
    private const float velocity = 700f;

    private void FixedUpdate()
    {
        transform.position += new Vector3(0f, 0, 0.001f) * velocity;
    }
}

  ```

  ## Demo 2

* PlayerPrefs
* PlayerPrefs editor

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo2.png"></td>

  </tr>
 </table>

   ```csharp

public class Demo2 : MonoBehaviour
{

    private TextMeshProUGUI txt_Variable;

    private void Awake()
    {
        txt_Variable = GameObject.Find("Txt_Variable").GetComponent<TextMeshProUGUI>();

        if (PlayerPrefs.HasKey("Variable"))
        {
            txt_Variable.text = PlayerPrefs.GetString("Variable");
        }
    }

    private void Start()
    {
        if (!PlayerPrefs.HasKey("Variable"))
        {
            PlayerPrefs.SetString("Variable", "This is variable !!!");
            PlayerPrefs.SetInt("Score", 9);
            PlayerPrefs.SetFloat("percentage", 0.67f);
        }
    }

}

  ```

## Demo 3

* DontDestroyOnLoad

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo3.png"></td>

  <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo3_2.png">
    </td>

  </tr>
 </table>

 ```csharp

public class Demo3_First : MonoBehaviour
{

    private Button btn_GoToScene2;

    private void Awake()
    {
        btn_GoToScene2 = GameObject.Find("Btn_GoToScene2").GetComponent<Button>();

        btn_GoToScene2.onClick.AddListener(delegate
        {
            SceneManager.LoadScene("Demo3_Second");
        });

    }
}

public class Demo3_Second : MonoBehaviour
{
    private Button btn_GoToScene1;

    private void Awake()
    {
        btn_GoToScene1 = GameObject.Find("Btn_GoToScene1").GetComponent<Button>();
        btn_GoToScene1.onClick.AddListener(GoToScene1);
    }

    private void GoToScene1()
    {
        SceneManager.LoadScene("Demo3_First");
    }
}


public class Demo3Manager : MonoBehaviour
{

    #region Singleton

    public static Demo3Manager Instance { get; private set; }

    private void Singleton()
    {
        if (Instance != null && Instance != this)
        {
            Destroy(this);
        }
        else
        {
            Instance = this;
            DontDestroyOnLoad(gameObject);
        }
    }
    #endregion

    private void Awake()
    {
        Debug.Log("Awake");

        Singleton();
    }

    private void Start()
    {
        StartCoroutine(DebugLogIEnumerator());
    }

    IEnumerator DebugLogIEnumerator()
    {
        var yieldReturn = new WaitForSeconds(0.3f);

        while (true)
        {
            yield return yieldReturn;
            Debug.Log("Demo3Manager");
        }
    }

}

  ```

  ## Demo 4

* Animator
* Animation Clip - Loop Time
* Animation Event
* Animation Speed

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo4.png"></td>

  </tr>
 </table>

 ```csharp

public class Demo4 : MonoBehaviour
{
    public void Trigger_AnimationEvent()
    {
        Debug.Log("I am at the ground...");
    }
}

  ```

  ## Demo 5

* Material
* Standart Shader

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo5.png"></td>

  </tr>
 </table>



  ## Demo 6

* Material
* Standart Shader

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo6.png"></td>

  </tr>
 </table>



  ## Demo 7

* Dotween

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo7.png"></td>

  </tr>
 </table>

 ```csharp

public class Demo7_Object1 : MonoBehaviour
{
    private void Start()
    {
        Tween tween =
         transform.DOMoveX(2f, 2f)
        .SetRelative(false) // move to relative position
        .SetEase(Ease.OutQuad)
        .SetDelay(5f)
        .SetSpeedBased(false) // zaman yerine hiz
        .SetId("PlayerMove")
        .SetLoops(5, LoopType.Yoyo);

        tween.onComplete = delegate { Debug.Log("onComplete"); };
        tween.onStepComplete = delegate { Debug.Log("onStepComplete"); };
        tween.onKill = delegate { Debug.Log("onKill"); };

        tween.Play();

        transform.DORotate(Vector3.up * 360, 2, RotateMode.FastBeyond360)
            .SetLoops(5, LoopType.Yoyo)
            .SetEase(Ease.Linear);
    }
}

  ```



  ## Demo 8

* Time class

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo8.png"></td>

  </tr>
 </table>

 ```csharp

public class Demo8 : MonoBehaviour
{

    private void Start()
    {
        StartCoroutine(DisplayCommandIEnumerator());
    }

    IEnumerator DisplayCommandIEnumerator()
    {
        var yieldReturn = new WaitForSeconds(1f);

        while (true)
        {
            yield return yieldReturn;

            Debug.Log($" Time.time {Time.time}");
            Debug.Log($" Time.realtimeSinceStartup {Time.realtimeSinceStartup}");
            Debug.Log($" Time.captureDeltaTime {Time.captureDeltaTime}");
            Debug.Log($" Time.fixedDeltaTime {Time.fixedDeltaTime}");
            Debug.Log($" Time.frameCount {Time.frameCount}");
            Debug.Log($" Time.deltaTime {Time.deltaTime}");
            Debug.Log($" Time.unscaledDeltaTime {Time.unscaledDeltaTime}");
            Debug.Log($" Time.captureFramerate {Time.captureFramerate}");
            Debug.Log($" Time.fixedTime {Time.fixedTime}");
            Debug.Log($" Time.unscaledTime {Time.unscaledTime}");
            Debug.Log($" Time.timeSinceLevelLoad {Time.timeSinceLevelLoad}");
            Debug.Log($" Time.timeAsDouble {Time.timeAsDouble}");
            Debug.Log($" Time.fixedUnscaledTimeAsDouble {Time.fixedUnscaledTimeAsDouble}");

        }
    }
}

  ```




  ## Demo 9

* Camera - Viewport Rect 

<table>

  <tr>
    <td><img src="https://raw.githubusercontent.com/bunyamineymen/Lesson2_DevelopingMobileGame/main/Assets/_Resources/demo9.png"></td>

  </tr>
 </table>