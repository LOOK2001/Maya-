```python
import sys
import fbx
import FbxCommon

inFileName = r'C:\Xicheng\Work\Project\Intern\Netease\Maya2Max\Models\test01.fbx'
outFileName = r'C:\Xicheng\Work\Project\Intern\Netease\Maya2Max\Models\outTest01.fbx'

def hierarchyNode(node):
    for i in range(node.GetChildCount()):
        hierarchyNode(node.GetChild(i))
        print node.GetChild(i).GetName()


def main():
    fbxManager = fbx.FbxManager.Create()
    fbxScene = fbx.FbxScene.Create(fbxManager, "")
    fbxImporter = fbx.FbxImporter.Create(fbxManager, "")
    fbxImporter.Initialize(outFileName)
    fbxImporter.Import(fbxScene)
    fbxRoot = fbxScene.GetRootNode()

    for i in range(fbxRoot.GetChildCount()):
        objectName = fbxRoot.GetChild(i).GetName()
        print objectName
        #hierarchyNode(fbxRoot.GetChild(i))

        object = fbxRoot.GetChild(i)
        objMatrix = object.EvaluateLocalScaling()
        print object.EvaluateLocalScaling()
        #print object.EvaluateGlobalTransform().GetT()
        objMatrix *= 5.0
        print object.EvaluateLocalScaling()
        #print object.EvaluateGlobalTransform().GetT()

        #matName = fbxRoot.GetChild(i).GetMaterial(0).GetName()

    # Create an exporter
    ''''''
    fbxExporter = fbx.FbxExporter.Create(fbxManager, "")
    fbxExporter.Initialize(outFileName)
    fbxExporter.Export(fbxScene)

main()
```



```python
import sys
import fbx
import FbxCommon

class FBX_Class(object):
    def __init__(self, filename):
        self.filename = filename
        self.scene = None
        self.sdk_manager = None
        self.sdk_manager, self.scene = FbxCommon.InitializeSdkObjects()
        FbxCommon.LoadScene(self.sdk_manager, self.scene, filename)

        self.root_node = self.scene.GetRootNode()

    def close(self):
        # destroy objects created by the sdk
        self.sdk_manager.Destroy()

    def save(self, filename = None):
        if not filename is None:
            FbxCommon.SaveScene(self.sdk_manager, self.scene, filename)
        else:
            FbxCommon.SaveScene(self.sdk_manager, self.scene, self.in_filename)
        self.close()

    def scale_by_value(self, value):
        for i in range(self.root_node.GetChildCount()):
            object = self.root_node.GetChild(i)
            print object.GetName()

            objMatrix = object.EvaluateLocalScaling()
            print object.EvaluateLocalScaling()
            objMatrix *= 5.0
            print object.EvaluateLocalScaling()

fbx_file = FBX_Class(r'C:\Xicheng\Work\Project\Intern\Netease\Maya2Max\Models\test01.fbx')
fbx_file.scale_by_value(5.0)
fbx_file.save(r'C:\Xicheng\Work\Project\Intern\Netease\Maya2Max\Models\outTest01.fbx')
```

