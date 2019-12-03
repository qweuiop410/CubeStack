### README.md

<img src="https://postfiles.pstatic.net/MjAxOTEyMDRfMTI1/MDAxNTc1NDAyNzY1MTIx.CxlPI1ROCsgoZ-4SmtKDzAnntUKvpgt-fyuAkr0rDJQg.pvxeS8jB6NlE-A4a3QlfB6WvfX5P2--ht72HCDhPubYg.PNG.whdals410/CubeStack_1.png?type=w773" width="40%" height="30%" title="px(픽셀) 크기 설정" alt="RubberDuck"></img>

+ 게임 'Cube Stack'을 따라 만들었습니다
+ 타이밍에 맞게 클릭해 큐브를 쌓아 올리는 게임입니다.
+ 쌓지 못했을때 다시 처음화면으로 돌아갑니다

+ 높이에 따라 큐브의 색 변경후 생성
``` csharp
private void SpawnTile()
    {
        lastTilePosition = theStack[stackIndex].transform.localPosition;
        stackIndex--;
        if (stackIndex < 0)
            stackIndex = transform.childCount - 1;

        desiredPosition = (Vector3.down) * scoreCount;
        theStack[stackIndex].transform.localPosition = new Vector3(0, scoreCount, 0);
        theStack[stackIndex].transform.localScale = new Vector3(stackBounds.x, 1, stackBounds.y);

        ColorMesh(theStack[stackIndex].GetComponent<MeshFilter>().mesh);
    }
    ```
    
    
 + 이동 방향 교차
 ``` csharp
  private void MoveTile()
    {
        tileTransition += Time.deltaTime * tileSpeed;
        if (isMovingOnX)
        {
            theStack[stackIndex].transform.localPosition = new Vector3(Mathf.Sin(tileTransition) * BOUNDS_SIZE, scoreCount, secondaryPosition);
        }
        else
        {
            theStack[stackIndex].transform.localPosition = new Vector3(secondaryPosition, scoreCount, Mathf.Sin(tileTransition) * BOUNDS_SIZE);
        }
    }
 ```
 
 + 지정 크기, 위치에 큐브 오브젝트 생성 
 ``` csharp
 private void CreateRubble(Vector3 pos, Vector3 scale)
    {
        GameObject go = GameObject.CreatePrimitive(PrimitiveType.Cube);
        go.transform.localPosition = pos;
        go.transform.localScale = scale;
        go.AddComponent<Rigidbody>();

        go.GetComponent<MeshRenderer>().material = stackMat;
        ColorMesh(go.GetComponent<MeshFilter>().mesh);
    }
 ```
    
