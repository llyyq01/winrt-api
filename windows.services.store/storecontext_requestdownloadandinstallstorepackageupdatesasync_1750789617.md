---
-api-id: M:Windows.Services.Store.StoreContext.RequestDownloadAndInstallStorePackageUpdatesAsync(Windows.Foundation.Collections.IIterable{Windows.Services.Store.StorePackageUpdate})
-api-type: winrt method
---

<!-- Method syntax
public Windows.Foundation.IAsyncOperationWithProgress<Windows.Services.Store.StorePackageUpdateResult, Windows.Services.Store.StorePackageUpdateStatus> RequestDownloadAndInstallStorePackageUpdatesAsync(Windows.Foundation.Collections.IIterable<Windows.Services.Store.StorePackageUpdate> storePackageUpdates)
-->

# Windows.Services.Store.StoreContext.RequestDownloadAndInstallStorePackageUpdatesAsync

## -description
Downloads and installs the specified package updates for the current app from the Windows Store.

## -parameters
### -param storePackageUpdates
The set of [StorePackageUpdate](storepackageupdate.md) objects that represent the updated packages to download and install.

## -returns
An object that the caller can observe to track progress and completion for the operation. On successful completion, the result is a [StorePackageUpdateResult](storepackageupdateresult.md) object that provides info about the package updates.

## -remarks
To get the list of packages that have updates available, use the [GetAppAndOptionalStorePackageUpdatesAsync](storecontext_getappandoptionalstorepackageupdatesasync.md) method. If you download a package update by using the [RequestDownloadStorePackageUpdatesAsync](storecontext_requestdownloadstorepackageupdatesasync.md) method before calling [RequestDownloadAndInstallStorePackageUpdatesAsync](storecontext_requestdownloadandinstallstorepackageupdatesasync.md), this method will install the package update without trying to download it again. For more information about using this method, including a code example, see [Download and install package updates for your app](https://msdn.microsoft.com/windows/uwp/packaging/self-install-package-updates).

This operation will not block. The [IAsyncOperationWithProgress](../windows.foundation/iasyncoperationwithprogress_2.md) object returned by this method will complete after the update packages are downloaded and installed.

When you call this method, the OS displays the following UI:

  * The OS displays a dialog that tells the user that an app update is available to download and asks the user's permission to proceed with the download. If the user does not grant permission to start the download, the [OverallState](storepackageupdateresult_overallstate.md) property of the [StorePackageUpdateResult](storepackageupdateresult.md) return value has the value **Canceled**.

  * After the updated packages are downloaded, the OS displays another dialog that tells the user that the app update is waiting to be installed and asks the user's permission to proceed with the installation. This dialog warns the user that the app might need to restart. If the user does not grant permission to start the installation, the [OverallState](storepackageupdateresult_overallstate.md) property of the [StorePackageUpdateResult](storepackageupdateresult.md) return value has the value **Canceled**.

### Get and display progress info for the download and install

The method that you assign to handle [Progress](../windows.foundation/iasyncoperationwithprogress_2_progress.md) notifications is called one time for each step in the download and installation process for each package in this request. The [Progress](../windows.foundation/iasyncoperationwithprogress_2_progress.md) handler receives a [StorePackageUpdateStatus](storepackageupdatestatus.md) argument that provides info about the update package that raised the progress notification.

If you want to show a custom progress UI (such as a [ProgressBar](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.progressbar.aspx)) that provides status to the user, you can use the **PackageDownloadProgress** field of the [StorePackageUpdateStatus](storepackageupdatestatus.md) argument to get the current progress of each package download and install operation, represented by a value from 0.0 to 1.0. This value increases from 0.0 to 0.8 during the download, and then it increases from 0.8 to 1.0 during the install.

Therefore, if you map the percentage shown in your custom progress UI directly to the value of the **PackageDownloadProgress** field, be aware that your UI will show 80% when the package is finished downloading and the OS displays the installation dialog. If you want your custom progress UI to display 100% when the package is downloaded and ready to be installed, you can modify your code to assign 100% to your progress UI when the **PackageDownloadProgress** property reaches 0.8.


## -examples

## -see-also
[Download and install package updates for your app](https://msdn.microsoft.com/windows/uwp/packaging/self-install-package-updates), [StoreContext](storecontext.md), [StorePackageUpdateResult](storepackageupdateresult.md), [StorePackageUpdateStatus](storepackageupdatestatus.md)
