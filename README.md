# vfspp

vfspp - C++ Virtual File System 

Forked from yevgeniy-logachev/vfspp and removed everything except memory file system. 

## How To Build
Builds shared lib only.
```
cmake . 
make
```

## Example
```
#include "CVirtualFileSystem.h"
#include "CMemoryFileSystem.h"

using namespace vfspp;

int main()
{
	vfs_initialize();
    IFileSystemPtr mem_fs(new CMemoryFileSystem());
    mem_fs->Initialize();
    CVirtualFileSystemPtr vfs = vfs_get_global();
    vfs->AddFileSystem("/memory/", mem_fs);

	// Create memory file
    IFilePtr memFile = vfs->OpenFile(CFileInfo("/memory/file.txt"), IFile::ReadWrite);
    if (memFile && memFile->IsOpened())
    {
        char data[] = "The quick brown fox jumps over the lazy dog\n";
	    memFile->Write(reinterpret_cast<uint8_t*>(data), sizeof(data));
	    memFile->Close();
    }
    
    IFilePtr memFile2 = vfs->OpenFile(CFileInfo("/memory/file.txt"), IFile::In);
    if (memFile2 && memFile2->IsOpened())
    {
        char data[256];
        memFile->Read(reinterpret_cast<uint8_t*>(data), 256);
        printf("%s\n", data);
    }

    vfs_shutdown();
	return 0;
}
```



